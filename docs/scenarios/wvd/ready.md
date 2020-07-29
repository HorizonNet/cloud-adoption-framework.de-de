---
title: Zielzonen in Azure für Windows Virtual Desktop-Instanzen
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit den bewährten Methoden für die virtuelle Desktopmigration vertraut zu machen, mit denen die Komplexität reduziert und der Migrationsprozess standardisiert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 21ae5207c7d4df5ef29c8a7f99000cbbf670f684
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452626"
---
# <a name="windows-virtual-desktop-azure-landing-zone-review"></a>Überprüfen der Zielzone in Azure für Windows Virtual Desktop

Vor der Migration zu Windows Virtual Desktop (WVD) benötigt das Team eine Azure-Zielzone, in der Desktops sowie unterstützende Workloads gehostet werden können. Die folgende Checkliste unterstützt Sie bei der Bewertung einer Zielzone im Hinblick auf deren Kompatibilität. Die Anleitung [Sicherstellen der Umgebungsbereitschaft für den Cloudeinführungsplan](../../ready/index.md) dieses Frameworks kann Sie bei der Erstellung einer kompatiblen Azure-Zielzone unterstützen, wenn keine bereitgestellt wurde.

## <a name="evaluate-compatibility"></a>Bewerten der Kompatibilität

- **Ressourcenorganisationsplan:** Die Zielzone sollte Verweise auf das Abonnement oder die Abonnements enthalten, die verwendet werden, eine Anleitung zur Verwendung der Ressourcengruppe und die Bezeichnungs- und Benennungsstandards, die für die Bereitstellung von Ressourcen verwendet werden sollen.
- **Azure AD:** Ein Azure Active Directory- oder Azure AD-Mandant sollte für die Endbenutzerauthentifizierung bereitgestellt werden.
- **Netzwerk**: Vor der Migration sollten erforderliche Netzwerkkonfigurationen in der Zielzone implementiert werden.
- **VPN oder ExpressRoute:** Außerdem ist für Zielzonen, die virtuelle Desktops unterstützen, eine Netzwerkverbindung für Endbenutzer erforderlich, damit diese eine Verbindung zur Zielzone und zu gehosteten Ressourcen herstellen können. Wenn für virtuelle Desktops bereits mehrere Endpunkte konfiguriert wurden, können Endbenutzer weiterhin über ein VPN oder eine ExpressRoute-Verbindung auf diese lokalen Geräte weitergeleitet werden. Wenn noch keine Endpunkte konfiguriert wurden, sollten Sie sich die Anleitung zum Konfigurieren von Netzwerkkonnektivitätsoptionen im Artikel [Sicherstellen der Umgebungsbereitschaft für den Cloudeinführungsplan](../../ready/index.md) ansehen.
- **Governance, Benutzer und Identität:** Sämtliche Anforderungen, um den Zugriff auf virtuelle Desktops zu steuern, sowie Anforderungen, Benutzer und Identitäten zu steuern, sollten als Azure-Richtlinien konfiguriert und auf die Zielzone angewendet werden, um Konsistenz gewährleisten zu können.
- **Sicherheit**: Das Sicherheitsteam hat die Zielzonenkonfigurationen überprüft und die einzelnen zur Verwendung vorgesehenen Zielzonen genehmigt, einschließlich der Zielzonen für die externe Verbindung und Zielzonen für unternehmenskritische Anwendungen oder vertrauliche Daten.
- **Windows Virtual Desktop (WVD):** Der PaaS-Dienst in WVD wurde aktiviert. <!-- TODO: Add link to enable the service. -->

Zielzonen, die mithilfe der Best Practices im Artikel [Sicherstellen der Umgebungsbereitschaft für den Cloudeinführungsplan](../../ready/index.md) entwickelt wurden, die die oben aufgeführten speziellen Anforderungen erfüllen können, wären als geeignete Zielzone für diese Migration geeignet.

Ein besseres Verständnis für eine Architektur in Windows Virtual Desktop finden Sie unter [Anforderungen](https://docs.microsoft.com/azure/virtual-desktop/overview#requirements).

## <a name="next-step-complete-a-windows-virtual-desktop-proof-of-concept"></a>Nächster Schritt: Durchführen eines Proof of Concept für Windows Virtual Desktop

- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
