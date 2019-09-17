---
title: Bewährte Methoden für die Azure-Bereitschaft
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einführung in bewährte Methoden für die Azure-Bereitschaft
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 275342d452c3f9c47c004014d6e2831c88aa91df
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022238"
---
# <a name="best-practices-for-azure-readiness"></a>Bewährte Methoden für die Azure-Bereitschaft

Mitarbeitern die notwendigen technischen Kenntnisse für die Cloudeinführung zu vermitteln, die sie benötigen, um die Zielumgebung für die Ressourcen und Workloads vorzubereiten, die in die Cloud migriert werden sollen, macht einen großen Teil der Vorbereitung für die Cloud aus. In den folgenden Themen finden Sie bewährte Methoden und zusätzliche Anleitungen, um Ihr Team bei der Einrichtung und Vorbereitung Ihrer Azure-Umgebung zu unterstützen.

## <a name="azure-fundamentals"></a>Azure-Grundlagen

Die folgenden Artikel enthalten hilfreiche Informationen zur Strukturierung und Bereitstellung von Ressourcen in der Azure-Umgebung:

- [Grundlegende Konzepte in Azure](../considerations/fundamental-concepts.md). Hier finden Sie Informationen zu grundlegenden Konzepten und Begriffen in Azure. Außerdem erfahren Sie hier, wie diese Konzepte zusammenhängen.
- [Empfohlene Namens- und Kennzeichnungskonventionen](../considerations/naming-and-tagging.md). Sehen Sie sich detaillierte Empfehlungen zur Benennung und Kennzeichnung Ihrer Ressourcen an. Diese Empfehlungen unterstützen Cloudeinführungsprojekte im Unternehmen.
- [Skalieren mit mehreren Azure-Abonnements](../considerations/scaling-subscriptions.md). Hier werden Strategien für die Skalierung mit mehreren Azure-Abonnements erläutert.
- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) Hier erfahren Sie, wie Azure-Verwaltungsgruppen zum Verwalten von Ressourcen, Rollen, Richtlinien und Bereitstellungen für mehrere Abonnements verwendet werden können.
- [Schaffen von Hybrid Cloud-Konsistenz](../../infrastructure/misc/hybrid-consistency.md). Hier erfahren Sie, wie Sie Hybrid Cloud-Lösungen erstellen, die die Vorteile innovativer Cloudfeatures mit vielen praktischen Features der lokalen Verwaltung kombinieren.

## <a name="networking"></a>Netzwerk

Die folgenden Artikel enthalten hilfreiche Informationen dazu, wie Sie Ihre Cloudnetzwerkinfrastruktur auf die Unterstützung Ihrer Workloads vorbereiten:

- [Netzwerkentscheidungen](../considerations/network-decisions.md). Hier erfahren Sie, welche Netzwerkdienste, -tools und -architekturen am besten für die Workload-, Governance- und Konnektivitätsanforderungen Ihrer Organisation geeignet sind.
- [Planen virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie virtuelle Netzwerke basierend auf Ihren Anforderungen in Bezug auf Isolierung, Verbindung und Standort planen.
- [Bewährte Methoden für die Netzwerksicherheit](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier finden Sie bewährte Methoden für die Verwendung integrierter Azure-Funktionen zum Beheben allgemeiner Netzwerksicherheitsprobleme.
- [Umkreisnetzwerke](./perimeter-networks.md). Umkreisnetzwerke werden auch als DMZ (Demilitarized Zone) bezeichnet und sorgen für sichere Konnektivität zwischen Ihren Cloudnetzwerken und Ihren lokalen oder physischen Rechenzentrumsnetzwerken sowie für sichere Internetkonnektivität.
- [Hub-and-Spoke-Netzwerktopologie](./hub-spoke-network-topology.md). „Hub-and-Spoke“ ist ein Netzwerkmodell für eine effizientere Verwaltung gemeinsamer Kommunikations- oder Sicherheitsanforderungen bei komplizierten Workloads. Es kann auch zur Beseitigung möglicher Azure-Abonnementeinschränkungen eingesetzt werden.

## <a name="identity-and-access-control"></a>Identität und Zugriffssteuerung

Nutzen Sie beim Entwerfen Ihrer Identitäts- und Zugriffssteuerungsinfrastruktur die folgenden Informationen, um die Sicherheit und Verwaltungseffizienz Ihrer Workloads zu optimieren:

- [Azure-Identitätsverwaltung und Sicherheit der Zugriffssteuerung – Bewährte Methoden](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier werden einige bewährte Methoden zur Identitätsverwaltung und Zugriffssteuerung mit integrierten Azure-Funktionen beschrieben.
- [Best Practices für die rollenbasierte Zugriffssteuerung](./roles.md). Die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) in Azure ermöglicht eine präzise gruppenbasierte Zugriffsverwaltung für Ressourcen, deren Struktur auf Benutzerrollen basiert.
- [Schützen des privilegierten Zugriffs für hybride und Cloudbereitstellungen in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Stellen Sie mithilfe von Azure Active Directory sicher, dass der Administratorzugriff und die Administratorkonten Ihrer Organisation sowohl in der Cloudumgebung als auch in der lokalen Umgebung sicher sind.

## <a name="storage"></a>Storage

- [Leitfaden zu Azure Storage](../considerations/storage-guidance.md). Wählen Sie die richtige Azure Storage-Lösung für Ihre Verwendungsszenarien aus.
- [Azure Storage-Sicherheitsleitfaden](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier finden Sie Informationen zu den Sicherheitsfeatures in Azure Storage.

## <a name="databases"></a>Datenbanken

- [Auswählen der richtigen SQL Server-Option in Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie die PaaS- oder IaaS-Lösung auswählen, die am besten für Ihre SQL Server-Workloads geeignet ist.
- [Bewährte Methoden für die Datenbanksicherheit](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier finden Sie bewährte Methoden für die Datenbanksicherheit auf der Azure-Plattform.
- [Auswählen des richtigen Datenspeichers:](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) Die Wahl des richtigen Datenspeichers für Ihre Anforderungen ist eine wichtige Entwurfsentscheidung. Es gibt buchstäblich Hunderte von Implementierungen, aus denen Sie unter SQL- und NoSQL-Datenbanken wählen können. Datenspeicher werden häufig nach der Strukturierung von Daten und den von ihnen unterstützten Betriebsarten kategorisiert. In diesem Artikel werden einige der gängigsten Speichermodelle beschrieben.

## <a name="cost-management"></a>Kostenverwaltung

- [Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen und Projekte](./track-costs.md). Hier finden Sie bewährte Methoden für die Erstellung sinnvoller Mechanismen zur Kostennachverfolgung.
- [Optimieren der Cloudinvestitionen mit Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie eine Strategie für die Kostenverwaltung implementieren und welche Tools zur Bewältigung von Herausforderungen im Zusammenhang mit Kosten zur Verfügung stehen.
- [Erstellen und Verwalten von Budgets](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie mit Azure Cost Management Budgets erstellen und verwalten.
- [Exportieren von Kostendaten](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie exportierte Daten in Azure Cost Management erstellen und verwalten.
- [Optimieren von Kosten anhand von Empfehlungen](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie mithilfe von Azure Cost Management und Azure Advisor nicht ausgelastete Ressourcen erkennen und geeignete Maßnahmen ergreifen, um die Kosten zu senken.
- [Verwenden von Kostenwarnungen zum Überwachen von Verbrauch und Ausgaben](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Hier erfahren Sie, wie Sie Ihre Azure-Nutzung und Ihre Ausgaben mithilfe von Cost Management-Warnungen überwachen.
