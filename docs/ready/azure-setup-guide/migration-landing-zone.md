---
title: Bereitstellen einer Landezone in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie in Azure eine Landezone für die Migration bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, setup
ms.openlocfilehash: 59b57467eeae47b73fa24ce672d9e7e4f0ed4478
ms.sourcegitcommit: 3655aa7f3e80249e0b2b562cd40dd750afc82043
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2019
ms.locfileid: "74251698"
---
# <a name="deploy-a-migration-landing-zone"></a>Bereitstellen einer Landezone für die Migration

Der Begriff *Landezone für die Migration* beschreibt eine Umgebung, die bereitgestellt und auf das Hosten von Workloads vorbereitet wurde, die von einer lokalen Umgebung nach Azure migriert werden. Eine Landezone für die Migration ist der letzte Baustein im Leitfaden für die Azure-Einrichtung. In diesem Artikel werden alle in diesem Leitfaden erläuterten Themen zur Bereitschaft zusammengefasst. Gleichzeitig werden die Entscheidungen angewendet, die Sie in Bezug auf die Bereitstellung Ihrer ersten Landezone für die Migration getroffen haben.

In den folgenden Abschnitten wird eine Landezone skizziert, die häufig verwendet wird, um eine Umgebung einzurichten, die sich für die Nutzung während einer Migration eignet. Die in diesem Artikel beschriebene Umgebung bzw. Landezone wurde auch in einer Azure-Blaupause zusammengefasst. Sie können die Blaupause für eine Landezone für die Migration von Cloud Adoption Framework (Framework für die Cloudeinführung) für eine Bereitstellung der definierten Umgebung mit einem einzigen Mausklick verwenden.

## <a name="purpose-of-the-blueprint"></a>Zweck der Blaupause

Die Blaupause für die Erstellung einer Landezone für die Migration von Cloud Adoption Framework (Framework für die Cloudeinführung) erstellt eine Landezone. Diese Landezone ist absichtlich eingeschränkt. Sie dient dazu, einen konsistenten Ausgangspunkt zu schaffen, der genügend Spielraum bietet, um das Konzept „Infrastruktur als Code“ kennenzulernen. Für einige Migrationsprojekte ist diese Landezone möglicherweise bereits ausreichend und erfüllt Ihre Anforderungen. Wahrscheinlich werden Sie aber auch einige Aspekte der Blaupause ändern müssen, um die einzigartigen Anforderungen Ihrer Organisation oder Ihres Unternehmens zu erfüllen.

## <a name="blueprint-alignment"></a>Einordnung der Blaupause

Die folgende Abbildung zeigt die Blaupause für eine Landezone für die Migration von Cloud Adoption Framework in Relation zur architektonischen Komplexität und zu den Complianceanforderungen.

![Einordnung der Blaupause](../../_images/ready/blueprint-overview.png)

- Der Buchstabe „A“ befindet sich innerhalb einer Kurvenlinie, die den Geltungsbereich dieser Blaupause kennzeichnet. Dieser Bereich macht deutlich, dass diese Blaupause sich nur für Architekturen mit geringer Komplexität eignet, aber im Hinblick auf Complianceanforderungen etwa in der Mitte liegt.
- Kunden mit einem hohen Maß an Komplexität und strikten Complianceanforderungen sind sicherlich besser bedient, wenn sie eine erweiterte Blaupause eines Partners oder eines der [standardbasierten Blaupausenbeispiele](https://docs.microsoft.com/azure/governance/blueprints/samples) verwenden.
- Die meisten Kunden liegen wahrscheinlich irgendwo zwischen diesen beiden Extremen. Der Buchstabe B repräsentiert den Prozess, der in den Artikeln zu [Überlegungen zu Landezonen](../considerations/index.md) skizziert wird. Kunden in diesem Bereich können die Entscheidungshilfen in diesen Artikeln verwenden, um Knoten zu ermitteln, die zur Blaupause für eine Landezone für die Migration von Cloud Adoption Framework hinzugefügt werden sollen. Dieser Ansatz ermöglicht Ihnen das Anpassen der Blaupause an Ihre Anforderungen.

## <a name="use-this-blueprint"></a>Verwenden dieser Blaupause

Bevor Sie die Blaupause für eine Landezone für die Migration von Cloud Adoption Framework verwenden, überprüfen Sie die folgenden Annahmen, Entscheidungen und Leitlinien für die Implementierung.

## <a name="assumptions"></a>Annahmen

Beim Definieren dieser anfänglichen Landezone galten folgende Annahmen bzw. Einschränkungen. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause zum Erstellen Ihrer ersten Landezone verwenden. Die Blaupause kann auch erweitert werden, sodass Sie eine Landezonenblaupause erstellen können, die Ihre einzigartigen Einschränkungen erfüllt.

- **Grenzwerte für Abonnements**: Bei der Einführung ist nicht damit zu rechnen, dass [Abonnementgrenzwerte](https://docs.microsoft.com/azure/azure-subscription-service-limits) überschritten werden. Zwei allgemeine Anzeichen dafür sind eine VM-Anzahl von über 25.000 oder eine vCPU-Anzahl von über 10.000.
- **Compliance**: In dieser Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Komponenten der Architektur**: Die Komplexität der Architektur erfordert keine zusätzlichen Produktionsabonnements.
- **Gemeinsam genutzte Dienste**: Es sind keine gemeinsam genutzten Dienste in Azure vorhanden, die erfordern, dass dieses Abonnement wie ein Spoke in einer Hub-and-Spoke-Architektur behandelt wird.

Wenn diese Annahmen mit Ihrer aktuellen Umgebung übereinstimmen, kann diese Blaupause ein guter Ausgangspunkt für die Erstellung Ihrer Landezone sein.

## <a name="decisions"></a>Entscheidungen

Die folgenden Entscheidungen werden in der Blaupause für die Landezone widergespiegelt.

| Komponente | Entscheidungen | Alternative Ansätze |
|---------|---------|---------|
|Migrationstools|Azure Site Recovery wird bereitgestellt, und ein Azure Migrate-Projekt wird erstellt.|[Entscheidungsleitfaden zur Wahl von Migrationstools](../../decision-guides/migrate-decision-guide/index.md)|
|Protokollierung und Überwachung|Ein Operational Insights-Arbeitsbereich und ein Speicherkonto für die Diagnose werden bereitgestellt.|         |
|Netzwerk|Es wird ein virtuelles Netzwerk mit Subnetzen für Gateway, Firewall, Jumpbox und Landezone erstellt.|[Netzwerkentscheidungen](../considerations/networking-options.md)|
|Identity|Es wird angenommen, dass das Abonnement bereits einer Azure Active Directory-Instanz zugeordnet ist.|[Bewährte Methoden für die Identitätsverwaltung](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json)         |
|Richtlinie|Bei dieser Blaupause wird derzeit davon ausgegangen, dass keine Azure-Richtlinien angewendet werden müssen.|         |
|Abonnemententwurf|N/V: wurde für ein einzelnes Produktionsabonnement entworfen.|[Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)|
|Verwaltungsgruppen|N/V: wurde für ein einzelnes Produktionsabonnement entworfen.|[Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)         |
|Ressourcengruppen|N/V: wurde für ein einzelnes Produktionsabonnement entworfen.|[Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)         |
|Data|–|[Auswählen der richtigen Bereitstellungsoption in Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) und [Auswählen des richtigen Datenspeichers](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Storage|–|[Leitfaden zu Azure Storage](../considerations/storage-options.md)         |
|Standards für Benennung und Kennzeichnung|–|[Best Practices zur Benennung und Kennzeichnung](../azure-best-practices/naming-and-tagging.md)         |
|Kostenverwaltung|–|[Nachverfolgen von Kosten](../azure-best-practices/track-costs.md)|
|Compute|–|[Computeoptionen](../considerations/compute-options.md)|

## <a name="customize-or-deploy-a-landing-zone-from-this-blueprint"></a>Anpassen oder Bereitstellen einer Landezone aus dieser Blaupause

Erfahren Sie mehr, und laden Sie aus den [Azure Blueprints-Beispielen](https://docs.microsoft.com/azure/governance/blueprints/samples) ein Referenzbeispiel der CAF-Blaupause (Cloud Adoption Framework, Framework für die Cloudeinführung) für eine Landezone für die Migration herunter, um sie bereitzustellen oder anzupassen.

Die Blaupausenbeispiele sind auch im Portal verfügbar. Ausführliche Informationen zum Erstellen einer Blaupause finden Sie unter [Azure Blueprints](./govern-org-compliance.md?tabs=azureblueprints#create-a-blueprint).

Eine Anleitung zu den Anpassungen, die in dieser Blaupause oder der resultierenden Landezone vorgenommen werden sollten, finden Sie in den Artikeln mit [Überlegungen zu Landezonen](../considerations/index.md).

## <a name="next-steps"></a>Nächste Schritte

Nachdem eine Migrationslandetone bereitgestellt wurde, können Sie Workloads zu Azure migrieren.
Anleitungen zu den Tools und Prozessen, die für die Migration Ihrer ersten Workload erforderlich sind, finden Sie im [Azure-Migrationsleitfaden](../../migrate/azure-migration-guide/index.md).

> [!div class="nextstepaction"]
> [Migrieren Ihrer ersten Workload mit dem Azure-Migrationsleitfaden](../../migrate/azure-migration-guide/index.md)
