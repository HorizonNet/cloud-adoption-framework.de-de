---
title: Zielzonen in Azure für Windows Virtual Desktop-Instanzen
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit den bewährten Methoden für die virtuelle Desktopmigration vertraut zu machen, mit denen die Komplexität reduziert und der Migrationsprozess standardisiert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4d554fa61572e26e880b437154d504a17b727772
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885268"
---
# <a name="windows-virtual-desktop-azure-landing-zone-review"></a>Überprüfen der Zielzone in Azure für Windows Virtual Desktop

Bevor das Contoso-Cloudeinführungsteam zu Windows Virtual Desktop migriert, benötigt es eine Azure-Zielzone, die in der Lage ist, Desktops und alle unterstützenden Workloads zu hosten. Die folgende Checkliste kann das Team bei der Bewertung einer Zielzone im Hinblick auf deren Kompatibilität unterstützen. Die Anleitung zur [Bereitschaftsmethodik](../../ready/index.md) dieses Frameworks kann das Team bei der Erstellung einer kompatiblen Azure-Zielzone unterstützen, wenn keine bereitgestellt wurde.

## <a name="evaluate-compatibility"></a>Bewerten der Kompatibilität

- **Ressourcenorganisationsplan:** Die Zielzone sollte Verweise auf das Abonnement oder die Abonnements enthalten, die verwendet werden, eine Anleitung zur Verwendung der Ressourcengruppe und die Bezeichnungs- und Benennungsstandards, die für die Bereitstellung von Ressourcen durch das Team verwendet werden sollen.
- **Azure AD:** Eine Azure Active Directory-Instanz (Azure AD) oder ein Azure AD-Mandant sollte für die Endbenutzerauthentifizierung bereitgestellt werden.
- **Netzwerk**: Vor der Migration sollten erforderliche Netzwerkkonfigurationen in der Zielzone implementiert werden.
- **VPN oder ExpressRoute:** Außerdem ist für Zielzonen, die virtuelle Desktops unterstützen, eine Netzwerkverbindung für Endbenutzer erforderlich, damit diese eine Verbindung mit der Zielzone und mit gehosteten Ressourcen herstellen können. Wenn für virtuelle Desktops bereits mehrere Endpunkte konfiguriert wurden, können Endbenutzer weiterhin über ein VPN oder eine Azure ExpressRoute-Verbindung auf diese lokalen Geräte weitergeleitet werden. Wenn noch keine Verbindung vorhanden ist, sollten Sie sich die Anleitung zum Konfigurieren von Netzwerkkonnektivitätsoptionen im Artikel [Sicherstellen der Umgebungsbereitschaft für den Cloudeinführungsplan](../../ready/index.md) ansehen.
- **Governance, Benutzer und Identität:** Sämtliche Anforderungen, um den Zugriff auf virtuelle Desktops zu steuern sowie Benutzer und ihre Identitäten zu steuern, sollten als Azure-Richtlinien konfiguriert und auf die Zielzone angewendet werden, um Konsistenz gewährleisten zu können.
- **Sicherheit**: Das Sicherheitsteam hat die Zielzonenkonfigurationen überprüft und die einzelnen zur Verwendung vorgesehenen Zielzonen genehmigt, einschließlich der Zielzonen für die externe Verbindung und Zielzonen für unternehmenskritische Anwendungen oder vertrauliche Daten.
- **Windows Virtual Desktop:** Platform-as-a-Service von Windows Virtual Desktop wurde aktiviert. <!-- TODO: Add link to enable the service. -->

Jede Zielzone, die das Team unter Anwendung der bewährten Methoden der [Bereitschaftsmethodik](../../ready/index.md) entwickelt und die die zuvor erwähnten bestimmten Anforderungen erfüllen kann, würde sich als Zielzone für diese Migration qualifizieren.

Ein besseres Verständnis für eine Architektur in Windows Virtual Desktop finden Sie unter den [Anforderungen für Windows Virtual Desktop](/azure/virtual-desktop/overview#requirements).

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
