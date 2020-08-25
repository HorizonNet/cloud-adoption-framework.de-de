---
title: Implementierungsoptionen für Zielzonen
description: Bestimmen Sie, welche Implementierungsoption für Zielzonen Ihren Anforderungen am besten gerecht wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: fada3a1485c470e04562365fe4f0a038c121708c
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88569653"
---
# <a name="landing-zone-implementation-options"></a>Implementierungsoptionen für Zielzonen

Mit [Azure-Zielzonen](./index.md) verfügen Cloudeinführungsteams über eine umfassend verwaltete Umgebung für ihre Workloads. Befolgen Sie den Leitfaden zu [Entwurfsbereichen für Zielzonen](./design-areas.md), um von diesen Funktionen zu profitieren.

Jede der folgenden Implementierungsoption ist für eine bestimmte Gruppe von Betriebsmodellabhängigkeiten konzipiert und unterstützt Ihre nicht funktionsbezogenen Anforderungen. Jede Implementierungsoption schließt eindeutig definierte Automatisierungsansätze ein. Sofern verfügbar, sind Referenzarchitekturen und Referenzimplementierungen eingeschlossen, mit denen Sie die Cloudeinführung beschleunigen können. Obwohl jede Option einem anderen Betriebsmodell zugeordnet ist, verwenden die Optionen dieselben Entwurfsbereiche. Der Unterschied besteht darin, wie Sie diese implementieren.

## <a name="platform-development-velocity"></a>Entwicklungsgeschwindigkeit der Plattform

Neben den empfohlenen Entwurfsbereichen ist die Entwicklungsgeschwindigkeit der Plattform (wie schnelle Ihr Plattformteam die erforderlichen Skills entwickeln kann) ein Schlüsselfaktor beim Auswählen der besten Bereitstellungsoption. Betrachten Sie zwei primäre Modi:

**Auf Unternehmensniveau beginnen:** Verwenden Sie diesen Modus, wenn Ihre Geschäftsanforderungen eine vielfältige Anfangsimplementierung von Zielzonen verlangen, mit vollständiger Integration von Governance, Sicherheit und Vorgängen von Anfang an. Mit diesem Ansatz können Sie entweder das Microsoft Azure-Portal oder Infrastructure-as-Code zum Einrichten und Konfigurieren Ihrer Umgebung verwenden. Sie können auch zwischen dem Portal und Infrastructure-as-Code wechseln (empfohlen), wenn Ihre Organisation bereit dafür ist. Infrastructure-as-Code-Ansätze setzen Kenntnisse in Bezug auf Azure Resource Manager-Vorlagen und GitHub voraus.

**Klein anfangen und erweitern:** Verwenden Sie diesen Modus, wenn es wichtiger ist, diese Fertigkeiten zu entwickeln und ihre Entscheidungen während Ihrer Einarbeitung in die Cloud zu treffen. Bei diesem Ansatz liegt der Fokus ausschließlich auf dem Implementieren der grundlegenden Aspekte der Zielzonen, die für den Einstieg in die Cloudeinführung erforderlich sind. Mit Ausweitung Ihrer Einführung bauen Module in den Governance- und Manage-Methodiken auf Ihren anfänglichen Zielzonen auf. Die Entwurfsprinzipien der einzelnen Azure-Zielzonen umfassen die spezifischen Entwurfsbereiche, die im Lauf der Zeit eine Umgestaltung erfordern.

## <a name="implementation-options"></a>Optionen für die Implementierung

In der folgenden Tabelle werden einige der Implementierungsoptionen für Zielzonen und die Variablen beschrieben, die Ihre Entscheidung beeinflussen könnten.

| Implementierungsoption | BESCHREIBUNG | Bereitstellungsgeschwindigkeit | Tiefere Entwurfsprinzipien | Anweisungen zur Bereitstellung |
|---|---|---|---|---|
| [Blaupause für die Zielzone der Cloud Adoption Framework-Migration](./migrate-landing-zone.md) | Stellt die Grundlage für das Migrieren von Ressourcen mit geringem Risiko dar. | Klein anfangen | [Entwurfsprinzipien](./migrate-landing-zone.md#design-principles) | [Bereitstellen](./migrate-landing-zone.md) |
| [Blaupause für die Cloud Adoption Framework-Grundlage](./foundation-blueprint.md) | Hiermit werden die Tools hinzugefügt, die für den Einstieg in die Entwicklung einer Governance-Strategie mindestens erforderlich sind. | Klein anfangen | [Entwurfsprinzipien](./foundation-blueprint.md#design-principles) | [Bereitstellen](./foundation-blueprint.md) |
| [CAF-Zielzone (Cloud Adoption Framework) auf Unternehmensebene](../enterprise-scale/index.md) | Stellt eine für Unternehmen geeignete Plattformgrundlage mit allen erforderlichen gemeinsamen Diensten zum Unterstützen des kompletten IT-Portfolios bereit. | Unternehmensebene | [Entwurfsprinzipien](../enterprise-scale/design-principles.md) | [Bereitstellen](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) |
| [Terraform-Module für das Cloud Adoption Framework](./terraform-landing-zone.md) | Drittanbieter-Pfad für Betriebsmodelle mit mehreren Clouds. Dieser Pfad kann zunächst von Azure ausgehende Betriebsmodelle beschränken. | Klein anfangen | [Entwurfsprinzipien](./terraform-landing-zone.md#design-decisions) | [Bereitstellen](./terraform-landing-zone.md#customize-and-deploy-your-first-landing-zone) |

In der folgenden Tabelle werden dieselben Implementierungsoptionen aus einem etwas anderen Blickwinkel betrachtet, um Entscheidungsprozesse mit eher technischen Entscheidungen zu erleichtern.

| Implementierungsoption | Hub | Spoke | Bereitstellungstechnologie | Anweisungen zur Bereitstellung |
|---|---|---|---|---|
| [CAF-Zielzone (Cloud Adoption Framework) auf Unternehmensebene](../enterprise-scale/index.md) | Enthalten  | Enthalten | Azure Resource Manager-Vorlagen, Azure-Portal, Azure Policy und GitHub | [Bereitstellen](../enterprise-scale/implementation-guidelines.md) |
| [Blaupause für die Zielzone der Cloud Adoption Framework-Migration](./migrate-landing-zone.md) | Refactoring erforderlich | Enthalten | Azure Resource Manager-Vorlagen, Azure-Portal und Azure Blueprints | [Bereitstellen](./migrate-landing-zone.md) |
| [Terraform-Module für das Cloud Adoption Framework](./terraform-landing-zone.md)  | Im Modul für virtuelle Rechenzentren enthalten | Enthalten | Terraform | [Bereitstellen](./terraform-landing-zone.md#customize-and-deploy-your-first-landing-zone) |

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie zum Fortfahren eine der in der vorstehenden Tabelle aufgeführten Implementierungsoptionen. Jede Option bietet einen Link zu einer Bereitstellungsanleitung und den spezifischen Entwurfsprinzipien, an denen sich die Implementierung orientiert.
