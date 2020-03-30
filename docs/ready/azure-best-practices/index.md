---
title: Bewährte Methoden für die Azure-Bereitschaft
description: Erfahren Sie mehr über bewährte Methoden und zusätzliche Anleitungen, um Ihr Team bei der Einrichtung und Vorbereitung Ihrer Azure-Umgebung zu unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: aecef0bbbdc88b2f95d6a93efeb496cf2d787a45
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354653"
---
# <a name="best-practices-for-azure-readiness"></a>Bewährte Methoden für die Azure-Bereitschaft

Zur Vorbereitung für die Cloud müssen Mitarbeitern die notwendigen technischen Kenntnisse für die Cloudeinführung vermittelt werden, die sie benötigen, um die Zielumgebung für die Ressourcen und Workloads vorzubereiten, die in die Cloud migriert werden sollen. Lesen Sie diese bewährten Methoden und zusätzliche Anleitungen, um Ihr Team bei der Vorbereitung Ihrer Azure-Umgebung zu unterstützen.

## <a name="azure-fundamentals"></a>Azure-Grundlagen

Organisieren und Bereitstellen Ihrer Ressourcen in der Azure-Umgebung.

- [Grundlegende Konzepte in Azure](../considerations/fundamental-concepts.md). Lernen Sie die wichtigsten Azure-Konzepte und Begriffe kennen, und erfahren Sie, wie diese Konzepte zusammenhängen.
- [Erstellen Sie Ihre anfänglichen Abonnements](./initial-subscriptions.md). Richten Sie einen anfänglichen Satz von Azure-Abonnements ein, um mit der Cloudeinführung zu beginnen.
- [Skalieren Sie Ihre Azure-Umgebung mit mehreren Abonnements](../azure-best-practices/scale-subscriptions.md). Machen Sie sich mit Gründen und Strategien für die Erstellung zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung vertraut.
- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](../azure-best-practices/organize-subscriptions.md) Hier erfahren Sie, wie Azure-Verwaltungsgruppen zum Verwalten von Ressourcen, Rollen, Richtlinien und Bereitstellungen für mehrere Abonnements verwendet werden können.
- [Halten Sie sich an empfohlene Namens- und Kennzeichnungskonventionen](../azure-best-practices/naming-and-tagging.md). Sehen Sie sich detaillierte Empfehlungen zur Benennung und Kennzeichnung Ihrer Ressourcen an. Diese Empfehlungen unterstützen Cloudeinführungsprojekte im Unternehmen.
- [Schaffen von Hybrid Cloud-Konsistenz](../considerations/hybrid-consistency.md). Hier erfahren Sie, wie Sie Hybrid Cloud-Lösungen erstellen, die die Vorteile innovativer Cloudfeatures mit vielen praktischen Features der lokalen Verwaltung kombinieren.

## <a name="networking"></a>Netzwerk

Bereiten Sie Ihre Cloudnetzwerkinfrastruktur auf die Unterstützung Ihrer Workloads vor.

- [Netzwerkentscheidungen](../considerations/networking-options.md). Hier erfahren Sie, welche Netzwerkdienste, -tools und -architekturen am besten für die Workload-, Governance- und Konnektivitätsanforderungen Ihrer Organisation geeignet sind.
- [Planen virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Planen Sie virtuelle Netzwerke basierend auf Ihren Anforderungen in Bezug auf Isolierung, Verbindung und Standort.
- [Bewährte Methoden für die Netzwerksicherheit](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier finden Sie bewährte Methoden für den Umgang mit allgemeinen Netzwerksicherheitsproblemen unter Verwendung integrierter Azure-Funktionen.
- [Umkreisnetzwerke](./perimeter-networks.md). Sorgen Sie für sichere Konnektivität zwischen Ihren Cloudnetzwerken und Ihren lokalen oder physischen Datencenternetzwerken (sowie für Internetkonnektivität).
- [Hub-and-Spoke-Netzwerktopologie.](./hub-spoke-network-topology.md) Verwalten Sie allgemeine Kommunikations- oder Sicherheitsanforderungen für komplizierte Workloads, und beheben Sie mögliche Einschränkungen des Azure-Abonnements.

## <a name="identity-and-access-control"></a>Identität und Zugriffssteuerung

Entwerfen Sie Ihre Identitäts- und Zugriffssteuerungsinfrastruktur, um die Sicherheit und Verwaltungseffizienz Ihrer Workloads zu optimieren.

- [Azure-Identitätsverwaltung und Sicherheit der Zugriffssteuerung – Bewährte Methoden](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier werden einige bewährte Methoden zur Identitätsverwaltung und Zugriffssteuerung mit integrierten Azure-Funktionen beschrieben.
- [Best Practices für die rollenbasierte Zugriffssteuerung](../considerations/roles.md). Ermöglichen Sie eine präzise gruppenbasierte Zugriffsverwaltung für Ressourcen, deren Struktur auf Benutzerrollen basiert.
- [Schützen des privilegierten Zugriffs für hybride und Cloudbereitstellungen in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Stellen Sie sicher, dass der Administratorzugriff und privilegierte Konten Ihrer Organisation sowohl in der Cloudumgebung als auch in der lokalen Umgebung sicher sind.

## <a name="storage"></a>Storage

- [Leitfaden zu Azure Storage](../considerations/storage-options.md). Wählen Sie die richtige Azure Storage-Lösung für Ihre Verwendungsszenarien aus.
- [Azure Storage-Sicherheitsleitfaden](https://docs.microsoft.com/azure/storage/blobs/security-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier finden Sie Informationen zu den Sicherheitsfeatures in Azure Storage.

## <a name="databases"></a>Datenbanken

- [Auswählen der richtigen SQL Server-Option in Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie die PaaS- oder IaaS-Lösung auswählen, die am besten für Ihre SQL Server-Workloads geeignet ist.
- [Bewährte Methoden für die Datenbanksicherheit](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier finden Sie bewährte Methoden für die Datenbanksicherheit auf der Azure-Plattform.
- [Auswählen des richtigen Datenspeichers:](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) Wählen Sie den richtigen Datenspeicher aus, um Ihre Anforderungen zu erfüllen. Es gibt Hunderte von Implementierungen, aus denen Sie unter SQL- und NoSQL-Datenbanken wählen können. Datenspeicher werden häufig nach der Strukturierung von Daten und den von ihnen unterstützten Betriebsarten kategorisiert. In diesem Artikel werden einige gängige Speichermodelle beschrieben.

## <a name="cost-management"></a>Kostenverwaltung

- [Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen und Projekte](./track-costs.md). Hier finden Sie bewährte Methoden für die Erstellung sinnvoller Mechanismen zur Kostennachverfolgung.
- [Optimieren der Cloudinvestitionen mit Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie eine Strategie für die Kostenverwaltung implementieren und welche Tools zur Bewältigung von Herausforderungen im Zusammenhang mit Kosten zur Verfügung stehen.
- [Erstellen und Verwalten von Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie mit Azure Cost Management Budgets erstellen und verwalten.
- [Exportieren von Kostendaten](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie mit Azure Cost Management Kostendaten exportieren.
- [Optimieren von Kosten anhand von Empfehlungen](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie mithilfe von Azure Cost Management und Azure Advisor nicht ausgelastete Ressourcen erkennen, um Kosten zu senken.
- [Verwenden von Kostenwarnungen zum Überwachen von Verbrauch und Ausgaben](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Hier erfahren Sie, wie Sie Ihre Azure-Nutzung und Ihre Ausgaben mithilfe von Cost Management-Warnungen überwachen.
