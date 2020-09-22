---
title: Proof of Concept für Windows Virtual Desktop
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität reduzieren und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b17c1703bd50f49e747a690ff9379a687a5543cf
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89605051"
---
<!-- cSpell:ignore FSLogix onboards remoteapp macos -->

# <a name="windows-virtual-desktop-proof-of-concept"></a>Proof of Concept für Windows Virtual Desktop

Bevor das Contoso-Team für die Cloudeinführung seine Endbenutzerdesktops bereitstellt, überprüft es die Konfiguration der Azure-Zielzone und die Netzwerkkapazität der Endbenutzer, indem es einen Proof of Concept ausfüllt und testet.

Der folgende Ansatz für den Migrationsprozess wird vereinfacht, um eine Proof of Concept-Implementierung zu beschreiben.

1. **Bewerten:** Das Team stellt Hostpools unter Verwendung der Standardgrößen virtueller Computer (virtual machines, VMs) bereit. Bewertungsdaten helfen dem Team dabei, die erwartete Anzahl von gleichzeitigen Benutzersitzungen und die Anzahl der VMs zu identifizieren, die zur Unterstützung dieser gleichzeitigen Sitzungen erforderlich sind.
2. **Bereitstellen:** Das Team [erstellt einen Hostpool](/azure/virtual-desktop/create-host-pools-azure-marketplace) für in Pools zusammengefasste Desktops unter Verwendung eines Windows 10-Katalogimages aus dem Azure Marketplace und der Dimensionierung aus dem Bewertungsschritt 1.
3. **Bereitstellen:** Das Team [erstellt RemoteApp-Anwendungsgruppen](/azure/virtual-desktop/manage-app-groups#create-a-remoteapp-group) für bereits migrierte Workloads.
4. **Bereitstellen:** Das Team [erstellt einen FSLogix-Profilcontainer](/azure/virtual-desktop/create-host-pools-user-profile) zum Speichern von Benutzerprofilen.
5. **Freigeben:** Das Team testet die Leistung und Wartezeit von Anwendungsgruppen und bereitgestellten Desktops für eine Stichprobe von Benutzern.
6. **Freigeben:** Das Team führt das Onboarding seiner Endbenutzer durch, um ihnen das Herstellen einer Verbindung über den [Windows Desktop-Client](/azure/virtual-desktop/connect-windows-7-and-10), [Webclient](/azure/virtual-desktop/connect-web), [Android-Client](/azure/virtual-desktop/connect-android), [macOS-Client](/azure/virtual-desktop/connect-macos) oder [iOS-Client](/azure/virtual-desktop/connect-ios) zu vermitteln.

## <a name="assumptions"></a>Annahmen

Der Proof of Concept-Ansatz kann einige Produktionsanforderungen erfüllen, aber er basiert auf einer Reihe von Annahmen.

Es ist unwahrscheinlich, dass sich alle folgenden Annahmen bei einer Unternehmensmigration von Windows Virtual Desktop als zutreffend erweisen werden. Das Adoption-Team sollte davon ausgehen, dass die Produktionsbereitstellung eine separate Bereitstellung erfordert, die den während der Windows Virtual Desktop-Bewertung identifizierten Produktionsanforderungen genauer entspricht. Die Annahmen sind:

- Endbenutzer haben eine Verbindung mit geringer Wartezeit mit der zugewiesenen Zielzone in Azure.
- Alle Benutzer können mit einem gemeinsam genutzten Pool von Desktops arbeiten.
- Alle Benutzer können das Windows&nbsp;10 Enterprise-Image mit mehreren Sitzungen aus Azure Marketplace verwenden.
- Alle Benutzerprofile werden entweder zu Azure Files, Azure NetApp Files oder zu einem VM-basierten Speicherdienst für die FSLogix-Profilcontainer migriert.
- Alle Benutzer können durch eine gemeinsame Persona mit einer Dichte von sechs Benutzern pro virtueller CPU (vCPU) und 4&nbsp;Gigabyte (GB) RAM beschrieben werden, [wie in den Größenempfehlungen für virtuelle Computer](/windows-server/remote/remote-desktop-services/virtual-machine-recs#multi-session-recommendations) angegeben.
- Alle Workloads sind mit Windows&nbsp;10-Mehrfachsitzungen kompatibel.
- Die Wartezeit zwischen den virtuellen Desktops und den Anwendungsgruppen ist für die Verwendung in der Produktion akzeptabel.

Das Team verwendet zum Berechnen der Kosten für das Windows Virtual Desktop-Szenario basierend auf der Proof of Concept-Konfigurationsreferenz den Preisrechner für [USA, Osten](https://azure.com/e/448606254c9a44f88798892bb8e0ef3c), [Europa, Westen](https://azure.com/e/61a376d5f5a641e8ac31d1884ade9e55)oder [Asien, Südosten](https://azure.com/e/7cf555068922461587d0aa99a476f926).
> [!NOTE]
> Diese Beispiele verwenden alle Azure Files als Speicherdienst für Benutzerprofile.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
