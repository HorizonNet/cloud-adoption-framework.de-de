---
title: Implementierungsoptionen für Zielzonen
description: Bestimmen Sie, welche Implementierungsoption für Zielzonen Ihren Anforderungen am besten gerecht wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 965f1a46bb3c44491528806cbc7af4a64d409039
ms.sourcegitcommit: 71a4f33546443d8c875265ac8fbaf3ab24ae8ab4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86479414"
---
# <a name="landing-zone-implementation-options"></a>Implementierungsoptionen für Zielzonen

Mit [Azure-Zielzonen](./index.md) verfügen Cloudeinführungsteams über eine umfassend verwaltete Umgebung für ihre Workloads. Befolgen Sie den Leitfaden zu [Entwurfsbereichen für Zielzonen](./design-areas.md), um von diesen Funktionen zu profitieren.

Jede Implementierungsoption unten ist für eine bestimmte Gruppe von Betriebsmodellabhängigkeiten konzipiert und unterstützt Ihre nicht funktionsbezogenen Anforderungen. Jede Implementierungsoption schließt eindeutig definierte Automatisierungsansätze ein. Sofern verfügbar, sind Referenzarchitekturen und Referenzimplementierungen eingeschlossen, mit denen Sie die Cloudeinführung beschleunigen können. Obwohl jede Option einem anderen Betriebsmodell zugeordnet ist, verwenden die Optionen dieselben Entwurfsbereiche. Der Unterschied besteht darin, wie Sie diese implementieren.

## <a name="platform-development-velocity"></a>Entwicklungsgeschwindigkeit der Plattform

Neben den empfohlenen Entwurfsbereichen ist die Entwicklungsgeschwindigkeit der Plattform (wie schnelle Ihr Plattformteam die erforderlichen Skills entwickeln kann) ein Schlüsselfaktor beim Auswählen der besten Bereitstellungsoption. Betrachten Sie zwei primäre Modi:

**Auf Unternehmensniveau beginnen:** Wenn Geschäftsanforderungen eine vielfältige Anfangsimplementierung von Zielzonen verlangen, mit vollständiger Integration von Governance, Sicherheit und Vorgängen von Anfang an, empfiehlt Microsoft den Ansatz auf Unternehmensniveau. Mit diesem Ansatz können Sie entweder das Microsoft Azure-Portal oder Infrastructure-as-Code zum Einrichten und Konfigurieren Ihrer Umgebung verwenden. Sie können auch zwischen dem Portal und Infrastructure-as-Code wechseln (empfohlen), wenn Ihre Organisation bereit dafür ist. Infrastructure-as-Code-Ansätze setzen Kenntnisse in Bezug auf Azure Resource Manager-Vorlagen und GitHub voraus.

**Klein anfangen und erweitern:** Wenn es wichtiger ist, diese Fertigkeiten zu entwickeln und ihre Entscheidungen während Ihrer Einarbeitung in die Cloud zu treffen, sollten Sie einen eher modularen Ansatz in Erwägung ziehen. Bei diesem Ansatz liegt der Fokus ausschließlich auf dem Implementieren der grundlegenden Aspekte der Zielzonen, die für den Einstieg in die Cloudeinführung erforderlich sind. Mit Ausweitung der Einführung bauen Module in den Governance- und Manage-Methodiken auf Ihren anfänglichen Zielzonen auf. Die Entwurfsprinzipien der einzelnen Azure-Zielzonen umfassen die spezifischen Entwurfsbereiche, die im Lauf der Zeit eine Umgestaltung erfordern.

## <a name="implementation-options"></a>Optionen für die Implementierung

Unten sind einige der Implementierungsoptionen für Zielzonen sowie die Variablen aufgeführt, die maßgebend für die Entscheidung sein können.

| Implementierungsoption | BESCHREIBUNG | Bereitstellungsgeschwindigkeit | Tiefere Entwurfsprinzipien | Anweisungen zur Bereitstellung |
|---|---|---|---|---|
| [Blaupause für die CAF-Migrationszielzone](./migrate-landing-zone.md) | Stellt die Grundlage für das Migrieren von Ressourcen mit geringem Risiko dar. | Klein anfangen | [Entwurfsprinzipien](./migrate-landing-zone.md#design-principles) | [Bereitstellen](./migrate-landing-zone.md) |
| [CAF-Basisblaupause](./foundation-blueprint.md) | Hiermit werden die Tools hinzugefügt, die für den Einstieg in die Entwicklung einer Governance-Strategie mindestens erforderlich sind. | Klein anfangen | [Entwurfsprinzipien](./foundation-blueprint.md#design-principles) | [Bereitstellen](./foundation-blueprint.md) |
| [CAF-Zielzone auf Unternehmensebene](../enterprise-scale/index.md) | Stellt eine für Unternehmen geeignete Plattformgrundlage mit allen erforderlichen gemeinsamen Diensten zum Unterstützen des kompletten IT-Portfolios bereit. | Unternehmensebene | [Entwurfsprinzipien](../enterprise-scale/design-principles.md) | [Bereitstellen](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) |
| [CAF-Terraform-Module](./terraform-landing-zone.md) | Drittanbieter-Pfad für Betriebsmodelle mit mehreren Clouds. Dieser Pfad kann zunächst von Azure ausgehende Betriebsmodelle beschränken. | Klein anfangen | [Entwurfsprinzipien](./terraform-landing-zone.md#design-decisions) | [Bereitstellen](./terraform-landing-zone.md#customize-and-deploy-your-first-landing-zone) |

In der folgenden Tabelle werden dieselben Implementierungsoptionen aus einem etwas anderen Blickwinkel betrachtet, um Entscheidungsprozesse mit eher technischen Entscheidungen zu erleichtern.

| Implementierungsoption | Hub | Spoke | Bereitstellungstechnologie | Anweisungen zur Bereitstellung |
|---|---|---|---|---|
| [CAF-Zielzone auf Unternehmensebene](../enterprise-scale/index.md) | Enthalten  | Enthalten | Azure Resource Manager-Vorlagen, Azure-Portal, Azure Policy und GitHub | [Bereitstellen](../enterprise-scale/implementation-guidelines.md) |
| [Blaupause für die CAF-Migrationszielzone](./migrate-landing-zone.md) | Refactoring erforderlich | Enthalten | Azure Resource Manager-Vorlagen, Azure-Portal und Azure Blueprints | [Bereitstellen](./migrate-landing-zone.md) |
| [CAF-Terraform-Module](./terraform-landing-zone.md)  | Im Modul für virtuelle Rechenzentren enthalten | Enthalten | Terraform | [Bereitstellen](./terraform-landing-zone.md#customize-and-deploy-your-first-landing-zone) |

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie eine der obigen Implementierungsoptionen aus, um fortzufahren. Jede Option bietet einen Link zu einer Bereitstellungsanleitung und den spezifischen Entwurfsprinzipien, an denen sich die Implementierung orientiert.
