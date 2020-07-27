---
title: Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration
description: Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a83c14475cc4d0c46e6c69e4061ea115e5b9b62b
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452745"
---
# <a name="ready-your-cloud-environment-for-azure-stack-hub-migration"></a>Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration

In diesem Artikel wird davon ausgegangen, dass Sie sich für die [Integration von Azure Stack in Ihre Cloudstrategie](./index.md) entschieden und einen [Plan für die Azure Stack Hub-Migration](./plan.md) entwickelt haben.

Bewerten Sie die Infrastrukturabhängigkeiten, die zuerst behandelt werden müssen:

- Identity
- Konnektivität
- Sicherheit
- Verschlüsselung

## <a name="hybrid-environment-configuration"></a>Hybridumgebungskonfiguration

Wenn Sie eine Hybridumgebung mit Teilen Ihres IT-Portfolios in der öffentlichen Cloud von Azure und anderen Teilen des Portfolios in der privaten Azure Stack Hub-Cloud entwerfen, sollten Sie zunächst einige grundlegende Dinge in der öffentlichen Cloud konfigurieren. Die Anleitungen in der [Bereitschaftsmethodik](../../ready/index.md) helfen Ihnen beim Einrichten von Zielzonen in der öffentlichen Cloud.

**Verbindungen mit Zielzone und Cloudplattform:** Stellen Sie während dieses Vorgangs sicher, dass Sie über eine stabile Netzwerkverbindung zwischen Ihrem aktuellen Rechenzentrum und Azure verfügen. Wenn die Netzwerkverbindung hergestellt wurde, testen Sie die Latenz, Bandbreite und Zuverlässigkeit der Verbindung mit Azure.

**Governance und Betrieb:** Bei der Migration zu beiden Clouds müssen Sie einige frühe Entscheidungen treffen, die sich auf die Umgebung auswirken. Bewährte Methoden basieren auf cloudnativen Vorgängen und Governancetools, die in der öffentlichen Cloud ausgeführt werden. Durch diesen Ansatz werden die Kosten für das Ausführen kostspieliger Systeme in Ihrem Rechenzentrum und das Belegen von Kapazität bei Azure Stack Hub verringert. Wenn Sie zu einer der beiden Formen von Azure-Clouds migrieren, müssen Sie sich entscheiden, ob Sie die bewährte Vorgehensweise befolgen oder weiterhin vorhandene Systeme für Betrieb, Governance und Change Management verwenden möchten.

## <a name="private-cloud-environment"></a>Private Cloudumgebung

Wenn Sie nur Azure Stack Hub verwenden möchten, die Version von Azure mit einer privaten Cloud, müssen Sie die gleichen Entscheidungspunkte in Erwägung ziehen.

**Lokale Governance und lokaler Betrieb:** Die bewährte Vorgehensweise bleibt weiterhin die Verwendung der cloudnativen Betriebs- und Governancetools für die Version von Azure mit öffentlicher Cloud. Diese empfohlenen Vorgehensweisen sollten unbedingt frühzeitig bewertet werden, um festzulegen, ob die bewährte Methode für Ihr Szenario gilt.

**Verbindungen mit Zielzone und Cloudplattform:** Wenn Ihre Workload-Migrationsvorgänge in Azure Stack Hub bereitgestellt werden sollen, müssen die Latenz, Bandbreite und Zuverlässigkeit der Netzwerkrouten zwischen den Endbenutzern und Ihrer Azure Stack-Appliance dokumentiert und getestet werden.

## <a name="next-step-assess-workloads-before-migration"></a>Nächster Schritt: Bewerten von Workloads vor der Migration

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney. Die im ersten Artikel beschriebene Bewertung von Workloads ist umfassender als die während des Planungsprozesses. Dadurch wird sichergestellt, dass Sie für die Migration der einzelnen Workloads bereit sind.

- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
