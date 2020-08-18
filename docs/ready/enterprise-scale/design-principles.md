---
title: Entwurfsprinzipien für das Cloud Adoption Framework auf Unternehmensebene
description: Erfahren Sie mehr über die Entwurfsprinzipien für die Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 25d11e5fafbf864790ae900154ca39f8b0569150
ms.sourcegitcommit: d31a9043d1ae9283ed126bf118ca26d1d18d6948
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88040625"
---
# <a name="cloud-adoption-framework-enterprise-scale-design-principles"></a>Entwurfsprinzipien für das Cloud Adoption Framework auf Unternehmensebene

Die in dieser Anleitung beschriebene Unternehmensarchitektur basiert auf den Entwurfsprinzipien, die hier beschrieben werden. Diese Prinzipien dienen als Kompass für nachfolgende Entwurfsentscheidungen, die für unternehmenskritische technische Bereiche getroffen werden müssen. Um die Auswirkungen und Nachteile zu verstehen, die auftreten, wenn diese Prinzipien nicht befolgt werden, sollten Sie sich intensiv mit den Prinzipien vertraut machen.

## <a name="subscription-democratization"></a>Demokratisierung von Abonnements

Abonnements sollten als Verwaltungseinheit verwendet und basierend auf den Anforderungen und Prioritäten eines Unternehmens skaliert werden. Sie werden eingesetzt, um Geschäftsbereiche und Portfoliobesitzer bei der Beschleunigung der Anwendungsmigration und der Entwicklung neuer Anwendungen zu unterstützen. Mithilfe von Abonnements sind Geschäftseinheiten in der Lage, neue Workloads zu entwerfen, zu entwickeln und zu testen sowie Workloads zu migrieren.

## <a name="policy-driven-governance"></a>Richtlinienbasierte Governance

Für eine kontinuierliche Konformität der Plattform Ihrer Organisation und der Anwendungen, die auf dieser Plattform bereitgestellt werden, sollte Azure Policy verwendet werden. Mit dieser Lösung profitieren Anwendungsbesitzer zudem von der notwendigen Eigenständigkeit und einem sicheren, ungehinderten Pfad zur Cloud.

## <a name="single-control-and-management-plane"></a>Eine einzige Steuerungs- und Verwaltungsebene

<!-- cSpell:ignore AppOps -->

Eine Architektur auf Unternehmensebene sollte keine Abstraktionsschichten wie beispielsweise vom Kunden entwickelte Portale oder Werkzeuge berücksichtigen. Es sollte sowohl für die AppOps (zentral verwaltete Betriebsteams) als auch für die DevOps (dedizierte Betriebsteams für Anwendungen) eine einheitliche Erfahrung bieten. Azure bietet eine einheitliche und konsistente Steuerungsebene für alle Azure-Ressourcen und Bereitstellungskanäle, die rollenbasierten Zugriffssteuerungen und richtlinienbasierten Steuerungen unterliegen. Azure kann dazu verwendet werden, eine standardisierte Reihe von Richtlinien und Steuerelementen für die Verwaltung der gesamten Unternehmensumgebung festzulegen.

## <a name="application-centric-and-archetype-neutral"></a>Anwendungszentrisch und archetypneutral

Die Architektur auf Unternehmensebene sollte sich auf anwendungsorientierte Migrationen und Entwicklung und nicht auf reine per Lift & Shift migrierte Infrastrukturen wie das Verschieben virtueller Computer konzentrieren. Sie sollte nicht zwischen alten und neuen Anwendungen, Infrastruktur als Dienst oder Plattform als Dienstanwendungen unterscheiden. Schließlich sollte die Architektur eine sichere Grundlage für die Bereitstellung sämtlicher Anwendungstypen auf Ihrer Azure-Plattform bieten.

## <a name="align-azure-native-design-and-roadmaps"></a>Ausrichtung von nativen Azure-Entwürfen und Roadmaps

Der Architekturansatz auf Unternehmensebene befürwortet den Einsatz von nativen Azure-Plattformdiensten und -funktionen, sofern möglich. Dieser Ansatz sollte mit den Roadmaps der Azure-Plattform übereinstimmen, um sicherzustellen, dass neue Funktionen in Ihren Umgebungen verfügbar sind. Anhand der Roadmaps für die Azure-Plattform lassen sich die Migrationsstrategie und der Ablauf auf Unternehmensebene bestimmen.

## <a name="recommendations"></a>Empfehlungen

Rechnen Sie damit, dass nicht die gesamte Funktionalität umgehend verfügbar ist, da es unwahrscheinlich ist, dass sämtliche Funktionen bereits am ersten Tag benötigt werden. Verwenden Sie Vorschaudienste, und arbeiten Sie mit den Roadmaps für Dienste, um technische Hindernisse zu beseitigen.
