---
title: Bereitstellen von Windows Virtual Desktop in Azure
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität reduzieren und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 50fea7acb50b2f14cabea51bdc9a53fecdaf1595
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572576"
---
<!-- cSpell:ignore NTFS Logix -->

# <a name="windows-virtual-desktop-deployment-or-migration"></a>Bereitstellen oder Migrieren von Windows Virtual Desktop

In diesem Artikel wird davon ausgegangen, dass Sie einen [Plan für Windows Virtual Desktop erstellt](./plan.md), [die Anforderungen für die Desktopbereitstellung geprüft](./migrate-assess.md) sowie [einen Proof of Concept durchgeführt](./proof-of-concept.md) haben und jetzt bereit sind, Ihre Windows Virtual Desktop-Instanzen (WVD) zu migrieren oder bereitzustellen.

## <a name="initial-scope"></a>Anfangsbereich

Die Bereitstellung von Windows Virtual Desktop-Instanzen folgt einem Prozess, der dem [Proof of Concept](./proof-of-concept.md)-Prozess ähnlich ist. Verwenden Sie diesen Anfangsbereich als Grundlage, um die verschiedenen Änderungen des Bereichs zu erläutern, die für die Ausgabe der Bewertung erforderlich sind.

- [Erstellen Sie einen Hostpool](/azure/virtual-desktop/create-host-pools-azure-marketplace) für in Pools zusammengefasste Desktops, indem Sie ein Windows&nbsp;10-Katalogimage aus Azure Marketplace und die Dimensionierung aus Schritt 1 dieses Verfahrens verwenden.
- [Erstellen Sie RemoteApp-Anwendungsgruppen](/azure/virtual-desktop/manage-app-groups#create-a-remoteapp-group) für Workloads, die bereits migriert wurden.
- [Erstellen Sie einen FSLogix-Profilcontainer](/azure/virtual-desktop/create-host-pools-user-profile), um Benutzerprofile zu speichern.

Die Bereitstellung und Migration umfasst die Migration von Personas, Anwendungen und Benutzerprofilen. Abhängig von den Ergebnissen der Workloadbewertung können die einzelnen Migrationstasks variieren. In diesem Artikel wird erläutert, wie sich der Bereich auf der Grundlage des Feedbacks zur Bewertung ändern kann.

## <a name="iterative-methodology"></a>Iterative Methoden

Jede Persona wird voraussichtlich eine Iteration des zuvor beschriebenen anfänglichen Bereichs erfordern, was zu mehreren Hostpools führt. In Abhängigkeit von der Windows Virtual Desktop-Bewertung sollte das Einführungsteam anhand der Anzahl von Personas oder Benutzern pro Persona Iterationen definieren. Wenn Sie den Prozess in personagesteuerte Iterationen unterteilen, können Sie die Auswirkungen der Änderungsgeschwindigkeit auf das Unternehmen verringern und es dem Team ermöglichen, sich auf das richtige Testen oder Onboarding für die einzelnen Personapools zu konzentrieren.

## <a name="scope-considerations"></a>Überlegungen zum Bereich

Die folgenden Überlegungen sollten bei der Entwurfsdokumentation für jede zu migrierende oder bereitzustellende Personagruppe beachtet werden. Nachdem die Bereichsüberlegungen in den zuvor diskutierten [anfänglichen Bereich](#initial-scope) eingeflossen sind, kann die Bereitstellung oder Migration beginnen.

### <a name="azure-landing-zone-considerations"></a>Überlegungen zu Landezonen in Azure

Bevor Sie die Personagruppen bereitstellen, sollte in der Azure-Region eine Zielzone erstellt werden, die zur Unterstützung der einzelnen bereitzustellenden Persona erforderlich ist. Jede zugewiesene Zielzone sollte unter Berücksichtigung der [Anforderungen für die Zielzonenüberprüfung](./ready.md) bewertet werden.

Wenn die zugewiesene Azure-Zielzone nicht Ihre Anforderungen erfüllt, sollte der Bereich für alle zukünftigen Änderungen der Umgebung hinzugefügt werden.

### <a name="application-and-desktop-considerations"></a>Überlegungen zu Anwendungen und Desktops

Bei einigen Personas besteht möglicherweise eine Abhängigkeit von Legacylösungen, die nicht mit Windows&nbsp;10 Multi-Session kompatibel sind. Dann sind für diese Personas möglicherweise dedizierte Desktops erforderlich. Diese Abhängigkeit wird unter Umständen erst bei der Bereitstellung oder beim Testen entdeckt.

Wenn sie erst spät im Prozess entdeckt werden, sollten zukünftige Iterationen der Modernisierung oder Migration der Legacyanwendung zugewiesen werden. Dadurch werden die langfristigen Kosten für die Desktopdarstellung gesenkt. Diese zukünftigen Iterationen sollten unter Berücksichtigung der Auswirkungen auf die Preise durch die Modernisierung im Vergleich zu den zusätzlichen Kosten priorisiert und durchgeführt werden, die durch dedizierte Desktops entstehen. Um Pipelineunterbrechungen und die Realisierung von Geschäftsergebnissen zu vermeiden, sollte diese Priorisierung die aktuellen Iterationen nicht beeinträchtigen.

Einige Anwendungen erfordern möglicherweise eine Problembehandlung, Modernisierung oder Migration zu Azure, damit den Endbenutzern die gewünschten Funktionen zur Verfügung stehen. Diese Änderungen werden wahrscheinlich nach dem Release vorgenommen. Wenn stattdessen aber die Desktoplatenz die Geschäftsfunktionen beeinflussen kann, können durch die Anwendungsänderungen Blockierungsabhängigkeiten für die Migration einiger Personas entstehen.

### <a name="user-profile-considerations"></a>Überlegungen zu Benutzerprofilen

Für den [Anfangsbereich](#initial-scope) wird davon ausgegangen, dass Sie einen [VM-basierten Container für FSLogix-Benutzerprofile](/azure/virtual-desktop/create-host-pools-user-profile) verwenden.

Sie können [Azure NetApp Files verwenden, um Benutzerprofile zu hosten](/azure/virtual-desktop/create-fslogix-profile-container). Dies erfordert einige zusätzliche Schritte im Bereich, einschließlich:

- **Pro NetApp-Instanz**: Konfigurieren Sie NetApp-Dateien, -Volumes und Active Directory-Verbindungen.
- **Pro Host/Persona**: Konfigurieren Sie FSLogix auf Sitzungshost-VMs.
- **Pro Benutzer**: Weisen Sie der Hostsitzung Benutzer zu.

Sie können auch [Azure Files verwenden, um Benutzerprofile zu hosten](/azure/virtual-desktop/create-file-share). Dies erfordert einige zusätzliche Schritte im Bereich, einschließlich:

- **Pro Azure Files-Instanz**: Konfigurieren Sie das Speicherkonto, den Datenträgertyp und die Active Directory-Verbindung ([Active Directory Domain Services (AD DS) wird ebenfalls unterstützt](/azure/virtual-desktop/create-profile-container-adds)), weisen Sie einer Active Directory-Benutzergruppe die rollenbasierte Zugriffssteuerung zu, wenden Sie NTFS-Berechtigungen (New Technology File System) an, und rufen Sie den Zugriffsschlüssel für das Speicherkonto ab.
- **Pro Host/Persona**: Konfigurieren Sie FSLogix auf Sitzungshost-VMs.
- **Pro Benutzer**: Weisen Sie der Hostsitzung Benutzer zu.

Die Benutzerprofile für einige Personas oder Benutzer erfordern möglicherweise auch eine Datenmigration, die die Migration bestimmter Personas verzögern kann, bis Korrekturen an den Benutzerprofilen innerhalb Ihrer lokalen Active Directory-Instanz oder auf einzelnen Benutzerdesktops vorgenommen werden können. Diese Verzögerung könnte den Bereich außerhalb des Windows Virtual Desktop-Szenarios erheblich beeinträchtigen. Nach deren Behebung können der ursprüngliche Bereich und die vorhergehenden Ansätze wieder aufgenommen werden.

## <a name="deploy-or-migrate-windows-virtual-desktop"></a>Migrieren oder Bereitstellen von Windows Virtual Desktop

Wenn Sie sämtliche dieser Überlegungen bei Ihrem Produktionsbereich für die Windows Virtual Desktop-Migration oder -Bereitstellung berücksichtigen, kann der Prozess gestartet werden. Bei einem iterativen Rhythmus stellt das Einführungsteam nun Hostpools, Anwendungen und Benutzerprofile bereit. Nach Abschluss der Bereitstellungsvorgang kann der [Test und das Onboarding von Benutzern](./migrate-release.md) beginnen.

## <a name="next-steps"></a>Nächste Schritte

[Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
