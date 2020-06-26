---
title: Entwurfsprinzipien
description: Entwurfsprinzipien.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a0763c9ea511ff311e672bb469e0b5a0e3443e3c
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076922"
---
# <a name="design-principles"></a>Entwurfsprinzipien

Die in dieser Anleitung beschriebene Unternehmensarchitektur basiert auf den Entwurfsprinzipien, die in diesem Abschnitt beschrieben werden. Diese Prinzipien dienen als Kompass für nachfolgende Entwurfsentscheidungen, die für unternehmenskritische technische Bereiche getroffen werden müssen. Um die Auswirkungen und Nachteile zu verstehen, die auftreten, wenn diese Prinzipien nicht befolgt werden, sollten Sie sich intensiv mit den Prinzipien vertraut machen.

## <a name="subscription-democratization"></a>Demokratisierung von Abonnements

Abonnements sollten als Verwaltungseinheit verwendet und basierend auf den Anforderungen und Prioritäten eines Unternehmens skaliert werden. Sie werden eingesetzt, um Geschäftsbereiche und Portfoliobesitzer bei der Beschleunigung der Anwendungsmigration und der Entwicklung neuer Anwendungen zu unterstützen. Mithilfe von Abonnements sind Geschäftseinheiten in der Lage, neue Workloads zu entwerfen, zu entwickeln und zu testen sowie Workloads zu migrieren.

## <a name="policy-driven-governance"></a>Richtlinienbasierte Governance

Für eine kontinuierliche Konformität der Kundenplattform und der Anwendungen, die auf dieser Plattform bereitgestellt werden, sollte Microsoft Azure Policy verwendet werden. Mit dieser Lösung profitieren Anwendungsbesitzer zudem von der notwendigen Eigenständigkeit und einem sicheren, ungehinderten Pfad zur Cloud.

## <a name="single-control-and-management-plane"></a>Eine einzige Steuerungs- und Verwaltungsebene

<!-- cSpell:ignore AppOps -->

Bei Unternehmensarchitekturen sollten keine Abstraktionsschichten (z. B. vom Kunden entwickelte Portale oder Tools) berücksichtigt werden. Außerdem sollte eine einheitliche Oberfläche für AppOps (zentral verwaltete Betriebsteams) und DevOps (dedizierte Betriebsteams für Anwendungen) implementiert werden. Azure bietet eine einheitliche Steuerungsebene für alle Azure-Ressourcen und Bereitstellungskanäle, für die rollenbasierte Zugriffsrichtlinien und richtlinienbasierte Kontrollen gelten. Mit dieser Steuerungsebene lassen sich standardisierten Richtlinien und Kontrollen definieren, mit denen sich die gesamte Kundenumgebung steuern und kontrollieren lässt.

## <a name="application-centric-and-archetype-neutral"></a>Anwendungszentrisch und archetypneutral

Bei Unternehmensarchitekturen sollte der Schwerpunkt auf der anwendungszentrischen Migration und Entwicklung liegen. Lift-and-Shift-Migrationen, bei denen beispielsweise lediglich virtuelle Computer verschoben werden, sollten vermieden werden. Außerdem sollte nicht zwischen alten und neuen Anwendungen bzw. zwischen IaaS- (Infrastructure-as-a-Service) oder PaaS-Anwendungen (Platform-as-a-Service) unterschieden werden. Schließlich sollte die Architektur eine sichere Grundlage für die Bereitstellung sämtlicher Anwendungstypen auf der Azure-Plattform des Kunden bieten.

## <a name="aligning-azure-native-design-and-roadmaps"></a>Ausrichtung von nativen Azure-Entwürfen und Roadmaps

Der Ansatz der Unternehmensarchitektur sieht nach Möglichkeit die Verwendung von nativen Diensten und Funktionen der Azure-Plattform vor. Um sicherzustellen, dass neue Funktionen in Kundenumgebungen verfügbar sind, sollten diese Dienste und Funktionen den Roadmaps der Azure-Plattform entsprechen. Anhand der Roadmaps für die Azure-Plattform lassen sich die Migrationsstrategie und der Ablauf auf Unternehmensebene bestimmen.

## <a name="recommendations"></a>Empfehlungen

Rechnen Sie damit, dass nicht die gesamte Funktionalität umgehend verfügbar ist. Es ist unwahrscheinlich, dass sämtliche Funktionen bereits am ersten Tag benötigt werden. Verwenden Sie Vorschaudienste, und arbeiten Sie mit den Roadmaps für Dienste, falls technische Hindernisse auftreten.
