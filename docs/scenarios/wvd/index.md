---
title: Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen in Azure
description: Nutzen Sie die Best Practices von Cloud Adoption Framework, um Windows Virtual Desktop-Instanzen zu Azure zu migrieren oder in Azure bereitzustellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: abd2bc9e7c201938f13cc7bdc1210ced4eb4637c
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108440"
---
# <a name="migrate-or-deploy-windows-virtual-desktop-instances-to-azure"></a>Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen in Azure

Das Migrieren von Endbenutzerdesktops einer Organisation zur Cloud ist ein häufiges Szenario bei Cloudmigrationen. Auf diese Weise können Sie die Mitarbeiterproduktivität verbessern und die Migration verschiedener Workloads beschleunigen, um die Benutzerfreundlichkeit der Organisation zu unterstützen.

## <a name="strategy-and-motivations"></a>Strategie und Beweggründe

Der Beweggrund für die Migration virtueller Desktops sind in der Regel die folgenden allgemeinen Zielergebnisse:

![Liste der Beweggründe für die Migration virtueller Desktops](../../_images/migrate/wvd/motivations.png)

- Organisationen möchten die Produktivität auf PCs, Smartphones, Tablets oder Browser ausdehnen, die möglicherweise nicht direkt der Kontrolle des IT-Teams unterliegen.
- Mitarbeiter müssen auf ihren Geräten auf Unternehmensdaten und -anwendungen zugreifen.
- Während Workloads zur Cloud migriert werden, ist mehr Unterstützung für Mitarbeiter erforderlich, um eine optimierte Umgebung und kurze Wartezeiten sicherzustellen.
- Die Kosten für die aktuellen oder vorgeschlagenen virtuellen Desktopumgebungen müssen optimiert werden, um Organisationen bei der effektiveren Skalierung Ihrer Remotearbeit zu unterstützen.
- Das IT-Team möchte den Arbeitsplatz modernisieren, und dieser Prozess beginnt häufig mit einer Transformation der Mitarbeitererfahrung.

Die Virtualisierung der Endbenutzerdesktops in der Cloud kann dem Team beim Erzielen dieser Ergebnisse helfen.

## <a name="approach-windows-virtual-desktop-refactor-and-modernization"></a>Ansatz: Umgestaltung und Modernisierung von Windows Virtual Desktop

Bei dem in diesem Artikel beschriebenen Ansatz werden die vorhandenen Citrix-, VMware- oder Remotedesktopdienst-Farmen modernisiert und durch eine PaaS-Lösung (Platform-as-a-Service) namens Windows Virtual Desktop ersetzt.

In diesem Szenario werden Desktopimages entweder zu Azure migriert, oder es werden neue Images generiert. Ebenso werden Benutzerprofile entweder zu Azure migriert, oder es werden neue Profile erstellt. Die Clientlösung wird bei der Migration größtenteils aktiviert, bleibt jedoch weitgehend unverändert.

![Diagramm für das Szenario der Migration virtueller Desktops](../../_images/migrate/wvd/scenario-solution.png)

Nach der Migration zur Cloud entfallen der Aufwand und die Kosten für die Verwaltung einer Farm mit virtuellen Desktops. Stattdessen verwaltet eine cloudnative Lösung die virtuelle Desktopumgebung für Ihr Team. Das Team muss sich lediglich um den Support für die Desktopimages, verfügbaren Anwendungen, Azure Active Directory und Benutzerprofile kümmern.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Planen der Windows Virtual Desktop-Migration oder -Bereitstellung](./plan.md)
- [Überprüfen Ihrer Umgebung oder Azure-Zielzone(n)](./ready.md)
- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
