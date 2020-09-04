---
title: Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration
description: Bereiten Sie Ihre Cloudumgebung für die Azure Stack Hub-Migration vor.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 5bd33e4e61dbef039b8d993606596fb707d66085
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885387"
---
# <a name="ready-your-cloud-environment-for-azure-stack-hub-migration"></a>Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration

In diesem Artikel wird davon ausgegangen, dass Sie sich für die [Integration von Azure Stack in Ihre Cloudstrategie](./index.md) entschieden und einen [Plan für die Azure Stack Hub-Migration](./plan.md) entwickelt haben.

Bewerten Sie die Infrastrukturabhängigkeiten, die zuerst behandelt werden müssen:

- Identity
- Konnektivität
- Sicherheit
- Verschlüsselung

## <a name="hybrid-environment-configuration"></a>Hybridumgebungskonfiguration

In einer Hybridumgebung befinden sich einige Teile Ihres IT-Portfolios in der öffentlichen Azure-Cloud und andere in der privaten Azure Stack Hub-Cloud. Für die Entwicklung einer solchen Umgebung sollten Sie zunächst einige grundlegende Elemente in der öffentlichen Cloud konfigurieren. Informationen zur Einrichtung von Zielzonen in der öffentlichen Cloud finden Sie unter [Sicherstellen der Vorbereitung Ihrer Umgebung auf die Cloudeinführung](../../ready/index.md).

**Verbindungen mit Zielzone und Cloudplattform**: Stellen Sie während des Vorgangs sicher, dass Sie über eine stabile Netzwerkverbindung zwischen Ihrem aktuellen Rechenzentrum und Azure verfügen. Nachdem Sie die Netzwerkverbindung hergestellt haben, testen Sie die Latenz, Bandbreite und Zuverlässigkeit der Verbindung mit Azure.

**Governance und Betrieb**: Bei der Migration zu beiden Clouds müssen Sie einige frühe Entscheidungen treffen, die sich auf die Umgebung auswirken. Durch die Anwendung bewährter Methoden setzen Sie auf cloudnativen Vorgängen und Governancetools auf, die in der öffentlichen Cloud ausgeführt werden. Durch diesen Ansatz werden die Kosten für das Ausführen kostspieliger Systeme in Ihrem Rechenzentrum und das Belegen von Kapazität bei Azure Stack Hub verringert. Wenn Sie zu einer der beiden Formen der Cloud migrieren, müssen Sie entweder bewährte Methoden befolgen oder weiterhin bestehende Systeme für Betrieb, Governance und Change Management verwenden.

## <a name="private-cloud-environment"></a>Private Cloudumgebung

Wenn Sie nur Azure Stack Hub verwenden möchten, die Version von Azure mit einer privaten Cloud, müssen Sie die gleichen Entscheidungspunkte in Erwägung ziehen:

**Lokale Governance und lokaler Betrieb**: Die bewährte Vorgehensweise bleibt weiterhin die Verwendung der cloudnativen Betriebs- und Governancetools für die Version von Azure mit öffentlicher Cloud. Es ist wichtig, diese bewährte Methode frühzeitig auszuwerten und festzustellen, ob sie auf Ihr Szenario anwendbar ist.

**Verbindungen mit Zielzone und Cloudplattform**: Wenn Ihre Workload-Migrationsvorgänge in Azure Stack Hub bereitgestellt werden sollen, müssen die Latenz, Bandbreite und Zuverlässigkeit der Netzwerkrouten zwischen den Endbenutzern und Ihrer Azure Stack-Appliance dokumentiert und getestet werden.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
