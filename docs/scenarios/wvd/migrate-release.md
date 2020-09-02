---
title: Aufgaben nach der Bereitstellung und Freigabe von Windows Virtual Desktop
description: Nutzen Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität verringern und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9389d3ec80422a5e17cfb6dd5a7692e2fd932fda
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885336"
---
# <a name="windows-virtual-desktop-post-deployment"></a>Nach der Bereitstellung von Windows Virtual Desktop

Der Freigabevorgang für die Migration oder Bereitstellung von Windows Virtual Desktop-Instanzen ist relativ unkompliziert. Dieses Verfahren entspricht dem beim [Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md):

- Testen der Leistung und Latenz von Anwendungsgruppen und bereitgestellten Desktops für eine Stichprobe von Benutzern
- Onboarding von Endbenutzern, um Ihnen das Herstellen folgender Verbindungsmöglichkeiten zu vermitteln:
  - [Windows-Desktopclient](/azure/virtual-desktop/connect-windows-7-and-10)
  - [Webclient](/azure/virtual-desktop/connect-web)
  - [Android-Client](/azure/virtual-desktop/connect-android)
  - [macOS-Client](/azure/virtual-desktop/connect-macos)
  - [iOS-Client](/azure/virtual-desktop/connect-ios)

## <a name="post-deployment"></a>Nach der Bereitstellung

Nach Abschluss der Freigabe werden häufig [Protokollierung und Diagnose für einen besseren Betrieb von Windows Virtual Desktop](/azure/virtual-desktop/diagnostics-log-analytics#push-diagnostics-data-to-your-workspace) hinzugefügt. Betriebsteams integrieren außerdem im Allgemeinen die in einem Pool zusammengefassten Hosts und virtuellen Desktop-Computern in die [bewährten Methoden für die Azure-Serververwaltung](../../manage/azure-server-management/index.md), um Berichte, Patches und Konfigurationen für Business Continuity & Disaster Recovery zu verwalten.

Obwohl der Freigabevorgang den Rahmen dieses Migrationsszenarios überschreitet, kann der Prozess jedoch die Notwendigkeit erkennbar machen, in nachfolgenden Durchläufen weitere Workloads zu Azure zu migrieren. Wenn Sie Microsoft 365 oder Azure Active Directory nicht konfiguriert haben, kann sich Ihr Cloudeinführungsteam nach der Veröffentlichung der Desktopszenarien für das Onboarding für diese Dienste entscheiden. In einem Hybridbetriebsmodell können die Betriebsteams auch Intune, System Center oder andere Konfigurationsverwaltungstools integrieren, um Betrieb, Compliance und Sicherheit zu verbessern.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die Migration von Windows Virtual Desktop abgeschlossen ist, kann Ihr Cloudeinführungsteam mit der nächsten szenariospezifischen Migration beginnen. Wenn Sie zusätzliche Desktops migrieren möchten, können Sie auch für die nächste Migration oder Bereitstellung von Windows Virtual Desktop noch einmal auf diese Artikelreihe zurückgreifen.

- [Planen der Windows Virtual Desktop-Migration oder -Bereitstellung](./plan.md)
- [Überprüfen Ihrer Umgebung oder der Azure-Zielzone](./ready.md)
- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
