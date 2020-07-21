---
title: Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen in Azure
description: Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen in Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 9c28afd9aa3bed856f66fb96e13a07b196f7dfdd
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451481"
---
# <a name="migrate-or-deploy-windows-virtual-desktop-instances-to-azure"></a>Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen in Azure

Das Migrieren von Endbenutzerdesktops zur Cloud ist ein häufiges Szenario bei Cloudmigrationen. Es ermöglicht Produktivitätssteigerungen und beschleunigt die Migration verschiedener Workloads, um die Endbenutzererfahrung zu unterstützen.

## <a name="strategy-and-motivations"></a>Strategie und Beweggründe

Der Beweggrund für Migrationen von virtuellen Desktops sind in der Regel die folgenden allgemeinen Zielergebnisse:

![Beweggründe für die Migration virtueller Desktops](../../_images/migrate/wvd/motivations.png)

- Es besteht der klare Wunsch, die Produktivität auf PCs, Smartphones, Tablets oder Browser auszudehnen, die möglicherweise nicht direkt der Kontrolle des IT-Teams unterliegen.
- Endbenutzer müssen auf ihren Geräten auf Unternehmensdaten und -anwendungen zugreifen.
- Während Workloads zur Cloud migriert werden, ist mehr Unterstützung für Endbenutzer erforderlich, um eine hohe Leistung und kurze Wartezeiten sicherzustellen.
- Die Kosten für die aktuellen oder vorgeschlagenen virtuellen Desktopumgebungen müssen optimiert werden, damit Sie die Kosten für Remotearbeit effektiv skalieren können.
- Das IT-Team möchte den Arbeitsplatz modernisieren, und dieser Prozess beginnt häufig mit einer Transformation der Endbenutzererfahrung.

Die Virtualisierung der Endbenutzerdesktops in der Cloud kann bei der Umsetzung jedes dieser Ziele helfen.

## <a name="approach-wvd-refactor-and-modernization"></a>Ansatz: Umgestaltung und Modernisierung mit Windows Virtual Desktop (WVD)

Bei dem in diesem Artikel beschriebenen Ansatz werden die vorhandenen Citrix-, VMware- oder Remotedesktopdienst-Farmen zur Verwendung einer Platform-as-a-Service-Lösung (PaaS) namens Windows Virtual Desktop (WVD) modernisiert.

Bei diesem Ansatz wird die Verwaltung virtueller Desktops modernisiert und durch Windows Virtual Desktop ersetzt, das Platform-as-a-Service-Angebot in Azure. Das Desktopimage wird entweder zu Azure migriert, oder es werden neue Images generiert. Das Benutzerprofil wird ebenfalls zu Azure migriert, oder es wird ein neues Profil erstellt. Die Clientlösung wird bei der Migration größtenteils aktiviert, bleibt jedoch weitgehend unverändert.

![Lösungsdiagramm für das Szenario der Migration virtueller Desktops](../../_images/migrate/wvd/scenario-solution.png)

Nach der Migration entfallen der Aufwand und die Kosten für die Verwaltung einer virtuellen Desktopfarm. Stattdessen verwaltet eine cloudnative Lösung die virtuelle Desktopumgebung für Kunden. Ihr Team muss sich lediglich um den Support für die Desktopimages, verfügbaren Anwendungen, Azure Active Directory und Benutzerprofile kümmern.

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Nächster Schritt: Integrieren dieser Strategie in Ihre Cloudeinführungsjourney

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Planen der Windows Virtual Desktop-Migration oder -Bereitstellung](./plan.md)
- [Überprüfen Ihrer Umgebung oder Azure-Zielzone(n)](./ready.md)
- [Durchführen eines Proof of Concept für Windows Virtual Desktop](./proof-of-concept.md)
- [Bewerten der Windows Virtual Desktop-Migration oder -Bereitstellung](./migrate-assess.md)
- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
