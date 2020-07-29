---
title: Proof of Concept für Windows Virtual Desktop
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit den bewährten Methoden für die virtuelle Desktopmigration vertraut zu machen, mit denen die Komplexität reduziert und der Migrationsprozess standardisiert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 00419cc14952f2a4b0faf1f986af50e086c8ffa5
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452633"
---
# <a name="windows-virtual-desktop-proof-of-concept"></a>Proof of Concept für Windows Virtual Desktop

Vervollständigen und testen Sie vor der Bereitstellung des Endbenutzerdesktops einen Proof of Concept, um die Konfiguration der Azure-Zielzone und der Netzwerkkapazität des Endbenutzers zu überprüfen. Der folgende Ansatz für den Migrationsprozess wird vereinfacht, um eine Proof of Concept-Implementierung zu beschreiben.

1. **Bewerten:** Hostpools sollten mithilfe der Standard-VM-Größen bereitgestellt werden. Bewertungsdaten helfen dabei, die erwartete Anzahl von gleichzeitigen Benutzersitzungen und die Anzahl der VMs zu identifizieren, die zur Unterstützung dieser gleichzeitigen Sitzungen erforderlich sind.
2. **Bereitstellen:** [Erstellen eines Hostpools](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace) für gepoolte Desktops, indem Sie ein Windows 10-Katalogimage aus dem Azure Marketplace und die Größenänderung aus Schritt 1 verwenden
3. **Bereitstellen:** [Erstellen von RemoteApp-Anwendungsgruppen](https://docs.microsoft.com/azure/virtual-desktop/manage-app-groups#create-a-remoteapp-group) für Workloads, die bereits migriert wurden
4. **Bereitstellen:** [Erstellen eines FSLogix-Profilcontainers](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-user-profile), um Benutzerprofile zu speichern
5. **Release:** Testen der Leistung und Wartezeit von Anwendungsgruppen und bereitgestellten Desktops für eine Stichprobe von Benutzern
6. **Release:** Integrieren von Endbenutzern, um Ihnen das Herstellen einer Verbindung über den [Windows Desktop-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-windows-7-and-10), [Webclient](https://docs.microsoft.com/azure/virtual-desktop/connect-web), [Android-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-android), [macOS-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-macos) oder [iOS-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-ios) zu vermitteln

## <a name="assumptions"></a>Annahmen

Der Proof of Concept-Ansatz kann einige Produktionsanforderungen erfüllen. Dieser Ansatz basiert jedoch auf einer Reihe von Annahmen.

Es ist unwahrscheinlich, dass sich die folgende Annahme für jede Unternehmensmigration von WVD als wahr erweist. Das Adoption-Team sollte davon ausgehen, dass die Produktionsbereitstellung eine separate Bereitstellung erfordert, die den während der Windows Virtual Desktop-Bewertung identifizierten Produktionsanforderungen genauer entspricht.

1. Endbenutzer haben eine Verbindung mit geringer Wartezeit mit der zugewiesenen Zielzone in Azure.
2. Alle Benutzer können mit einem gemeinsam genutzten Pool von Desktops arbeiten.
3. Alle Benutzer können das Windows 10 Enterprise-Image mit mehreren Sitzungen aus dem Azure Marketplace verwenden.
4. Alle Benutzerprofile werden entweder zu Azure Files, Azure NetApp Files oder zu einem VM-basierten Speicherdienst für die FSLogix-Profilcontainer migriert.
5. Alle Benutzer können [gemäß den Empfehlungen für die VM-Größenanpassung](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/virtual-machine-recs#multi-session-recommendations) durch eine gemeinsame Persona mit sechs Benutzern pro 1 vCPU und 4 GB RAM beschrieben werden.
6. Alle Workloads sind mit Windows 10-Mehrfachsitzungen kompatibel.
7. Die Wartezeit zwischen den virtuellen Desktops und den Anwendungsgruppen ist für die Verwendung in der Produktion akzeptabel.

Verwenden Sie zum Berechnen der Kosten für das WVD-Szenario basierend auf der Proof of Concept-Konfigurationsreferenz den Preisrechner für [USA, Osten](https://azure.com/e/448606254c9a44f88798892bb8e0ef3c), [Europa, Westen](https://azure.com/e/61a376d5f5a641e8ac31d1884ade9e55)oder [Asien, Südosten](https://azure.com/e/7cf555068922461587d0aa99a476f926). Hinweis: Diese Beispiele verwenden alle Azure Files, den Speicherdienst für die Speicherung von Benutzerprofilen.

## <a name="next-step-assess-for-windows-virtual-desktop"></a>Nächster Schritt: Bewerten für Windows Virtual Desktop

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
