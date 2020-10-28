---
title: Testgesteuerte Entwicklung für Zielzonen in Azure
description: Testgesteuerte Entwicklung für Zielzonen in Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b9d5cba7af85f88c0b7da841c18a490b49c120c9
ms.sourcegitcommit: 6aa14b15efc9bd351b75f8a3d7ebbac3d575275b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689890"
---
# <a name="test-driven-development-for-landing-zones-in-azure"></a>Testgesteuerte Entwicklung für Zielzonen in Azure

Wie im vorhergehenden Artikel über [testgesteuerte Entwicklung (Test-Driven Development, TDD) für Zielzonen](./test-driven-development.md) beschrieben, beginnen TDD-Zyklen mit einem Test, der die Akzeptanzkriterien eines bestimmten Features validiert, das für die Bereitstellung des Cloudeinführungsplans erforderlich ist. Die Erweiterung oder das Refactoring der Zielzone kann dann getestet werden, um zu bestätigen, dass die Akzeptanzkriterien erfüllt sind. In diesem Artikel wird eine cloudnative Toolkette in Azure vorgestellt, um testgesteuerte Entwicklungszyklen zu automatisieren.

## <a name="azure-tools-to-support-landing-zone-tdd-cycles"></a>Azure-Tools zur Unterstützung der TDD-Zyklen von Zielzonen

![Tools für die testgesteuerte Entwicklung in Azure](../../_images/ready/azure-tdd-tools.png)
_Abbildung 1: Tools für die testgesteuerte Entwicklung in Azure_

Die Toolkette der Azure-nativen Governanceprodukte und -dienste lässt sich problemlos in die testgesteuerte Entwicklung für die Erstellung von Zielzonen integrieren. Jedes dieser Tools dient einem bestimmten Zweck, wodurch die Entwicklung, das Testen und die Bereitstellung Ihrer Zielzone in Übereinstimmung mit TDD-Zyklen erleichtert wird.

## <a name="microsoft-provided-test-and-deployment-templates-to-accelerate-tdd"></a>Von Microsoft bereitgestellte Test- und Bereitstellungsvorlagen zum Beschleunigen von TDD

Die folgenden Beispiele werden von Microsoft für Governancezwecke zur Verfügung gestellt. Sie können jeweils als Test oder Testreihe in einem testgesteuerten Entwicklungszyklus für Zielzonen verwendet werden. Die folgenden Abschnitte enthalten weitere Informationen zu den einzelnen Tools:

- Azure Blueprints bietet verschiedene [Blaupausenbeispiele](/azure/governance/blueprints/samples), die Richtlinien für Tests und Vorlagen für die Bereitstellung enthalten. Diese Blaupausenmuster können den Entwicklungs-, Bereitstellungs- und Testaufwand in TDD-Zyklen beschleunigen.
- Azure Policy umfasst auch [integrierte Richtlinieninitiativen](/azure/governance/policy/samples/built-in-initiatives), die dazu dienen könnten, die vollständige „Definition of Done“ für eine Zielzone zu testen und durchzusetzen. Azure Policy umfasst [integrierte Richtliniendefinitionen](/azure/governance/policy/samples/built-in-policies), die individuelle Akzeptanzkriterien innerhalb der „Definition of Done“ erfüllen können.
- Azure Graph enthält fortgeschrittene [Abfragebeispiele](/azure/governance/resource-graph/samples/advanced), die für fortgeschrittene Testszenarien verwendet werden können, um zu verstehen, wie die Workloads innerhalb einer Zielzone bereitgestellt werden.
- [Azure-Schnellstartvorlagen](https://azure.microsoft.com/resources/templates) stellen Quellcodevorlagen zur Verfügung, um die Bereitstellung der Zielzone und der Workload zu beschleunigen.

Die oben angegebenen Beispiele können zur Beschleunigung von TDD-Zyklen verwendet werden. Sie werden mit den Governancetools in den folgenden Abschnitten ausgeführt und ermöglichen es Cloudplattformteams, ihren eigenen Quellcode und ihre eigenen Tests zu erstellen.

## <a name="azure-governance-tools-that-can-accelerate-tdd-cycles"></a>Azure Governance-Tools, die TDD-Zyklen beschleunigen können

[Azure Policy](/azure/governance/policy): Wenn die Bereitstellungen oder versuchten Bereitstellungen von den Governancerichtlinien abweichen, kann Azure Policy automatische Erkennung, Schutz und Lösung bieten. Aber Azure Policy bietet auch den primären Mechanismus zum Testen von Akzeptanzkriterien in Ihrer Definition of Done. In einem TDD-Zyklus kann eine Richtliniendefinition erstellt werden, um ein einzelnes Akzeptanzkriterium zu testen. Ebenso können alle Akzeptanzkriterien zu einer Richtlinieninitiative hinzugefügt werden, die dem gesamten Abonnement zugewiesen wird. Dieser Ansatz bietet einen Mechanismus für Rot-Tests, bevor die Zielzone geändert wird. Wenn die Zielzone der Definition of Done entspricht, kann sie zur Erzwingung der Testkriterien verwendet werden, um Codeänderungen zu vermeiden, die in zukünftigen Releases zu Testfehlern führen würden.

[Azure Blueprints](/azure/governance/blueprints): Azure Blueprint gruppiert Richtlinien und andere Bereitstellungstools in einem wiederholbaren Paket, das mehreren Zielzonen zugeordnet werden kann. Blaupausen erweisen sich als nützlich, wenn mehrere Einführungsbemühungen eine gemeinsame „Definition of Done“ aufweisen, die Sie im Laufe der Zeit vielleicht aktualisieren möchten. Sie können auch bei späteren Bemühungen zur Erweiterung und Umgestaltung von Zielzonen bei deren Bereitstellung helfen.

[Azure Resource Graph](/azure/governance/resource-graph/overview): Resource Graph bietet eine Abfragesprache zur Erstellung datengesteuerter Tests auf der Grundlage von Informationen über die in einer Zielzone bereitgestellten Ressourcen. Später im Einführungsplan kann dieses Tool auch komplexe Tests definieren, die auf den Interaktionen zwischen den Workloadressourcen und der zugrunde liegenden Cloudumgebung basieren.

[Azure Resource Manager-Vorlagen](/azure/azure-resource-manager/templates/overview): Diese Vorlagen stellen den primären Quellcode für jede in Azure bereitgestellte Umgebung zur Verfügung. Einige Drittanbietertools wie etwa Terraform generieren ihre eigenen ARM-Vorlagen, die dann an Azure Resource Manager übermittelt werden.

[Azure Resource Manager](/azure/azure-resource-manager/management/overview): Resource Manager bietet eine konsistente Plattform für den Aufbau und die Bereitstellung von Funktionen. Von dieser Plattform können Zielzonen auf der Grundlage von Quellcodedefinitionen bereitgestellt werden.

## <a name="next-steps"></a>Nächste Schritte

Bewerten Sie [grundlegende Überlegungen zu Zielzonen](./basic-considerations.md), um mit dem Refactoring Ihrer ersten Zielzone zu beginnen.

> [!div class="nextstepaction"]
> [Grundlegende Überlegungen zu Zielzonen](./basic-considerations.md)
