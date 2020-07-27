---
title: Aufgaben nach der Bereitstellung und Freigabe von Windows Virtual Desktop
description: Nutzen Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität verringern und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4c5c4140bb5735706f8cefbb4f37cdc391601c75
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452623"
---
# <a name="windows-virtual-desktop-post-deployment"></a>Nach der Bereitstellung von Windows Virtual Desktop

Der Freigabevorgang für die Migration oder Bereitstellung von Windows Virtual Desktop-Instanzen ist relativ unkompliziert. Dieses Verfahren entspricht dem beim [Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md):

- Testen der Leistung und Latenz von Anwendungsgruppen und bereitgestellten Desktops für eine Stichprobe von Benutzern
- Onboarding von Endbenutzern, um Ihnen das Herstellen folgender Verbindungsmöglichkeiten zu vermitteln:
  - [Windows-Desktopclient](https://docs.microsoft.com/azure/virtual-desktop/connect-windows-7-and-10)
  - [Webclient](https://docs.microsoft.com/azure/virtual-desktop/connect-web)
  - [Android-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-android)
  - [macOS-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-macos)
  - [iOS-Client](https://docs.microsoft.com/azure/virtual-desktop/connect-ios)

## <a name="post-deployment"></a>Nach der Bereitstellung

Nach Abschluss der Freigabe werden häufig [Protokollierung und Diagnose für einen besseren Betrieb von Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/diagnostics-log-analytics#push-diagnostics-data-to-your-workspace) hinzugefügt. Betriebsteams integrieren außerdem im Allgemeinen die in einem Pool zusammengefassten Hosts und Desktop-VMs in die [bewährten Methoden für die Azure-Serververwaltung](../../manage/azure-server-management/index.md), um Berichte, Patches und BCDR-Konfigurationen zu verwalten.

Der Freigabevorgang überschreitet den Rahmen dieses Migrationsszenarios, kann jedoch die Notwendigkeit erkennbar machen, in nachfolgenden Durchläufen weitere Workloads zu Azure zu migrieren. Wenn Sie Office 365 und Azure AD nicht konfiguriert haben, kann das Team nach der Freigabe von Desktopszenarien ein Onboarding dieser Dienste durchführen. In einem Hybridbetriebsmodell können die Betriebsteams auch Intune, System Center oder andere Konfigurationsverwaltungstools integrieren, um Betrieb, Compliance und Sicherheit zu verbessern.

## <a name="next-step-your-next-migration-iteration"></a>Nächster Schritt: Ihr nächster Migrationsdurchlauf

Nachdem die Migration von Windows Virtual Desktop abgeschlossen ist, kann das Cloudeinführungsteam mit der nächsten szenariospezifischen Migration beginnen. Wenn Sie zusätzliche Desktops migrieren möchten, können Sie auch für die nächste Migration oder Bereitstellung von Windows Virtual Desktop noch einmal auf diese Artikelreihe zurückgreifen.

- [Planen der Windows Virtual Desktop-Migration oder -Bereitstellung](./plan.md)
- [Überprüfen Ihrer Umgebung oder der Azure-Zielzone](./ready.md)
- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
