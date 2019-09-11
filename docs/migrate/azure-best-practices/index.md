---
title: Bewährte Methoden für die Azure-Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einführung in die bewährten Methoden für die Azure-Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e8a7ae0af3b64a6d7e04555fe64a6189d964b3ff
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816566"
---
# <a name="azure-migration-best-practices"></a>Bewährte Methoden für die Azure-Migration

Azure bietet mehrere Tools, die bei der Durchführung einer Migration helfen. Dieser Abschnitt des Cloud Adoption Framework soll den Lesern helfen, diese Tools in Übereinstimmung mit den bewährten Methoden für die Migration zu implementieren. Diese bewährten Methoden sind auf einen der Prozesse innerhalb des unten abgebildeten Migrationsmodells des Cloud Adoption Frameworks abgestimmt.

Erweitern Sie die einzelnen Prozesse im Inhaltsverzeichnis auf der linken Seite, um die für diesen Prozess typischen bewährten Methoden anzuzeigen.

![Cloud Adoption Framework-Migrationsmodell](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> Die Planung und Bewertung von digitalen Beständen und Ressourcen stellt zwei verschiedene Ebenen der Migrationsplanung und -bewertung dar:
>
> - **Planung digitaler Bestände:** Sie planen oder rationalisieren den digitalen Bestand während der Planung, um einen gesamten Backlog für die Migration aufzustellen. Dieser Plan basiert jedoch auf einigen Annahmen und Details, die vor der Migration eines Workloads überprüft werden müssen.
> - **Ressourcenbewertung:** Sie bewerten die einzelnen Ressourcen einer Workload vor ihrer Migration, um die Cloudkompatibilität zu bewerten und die Einschränkungen hinsichtlich Architektur und Skalierung zu verstehen. Dieser Prozess überprüft die anfänglichen Annahmen und liefert die Details, die für die Migration einer einzelnen Ressource erforderlich sind.
