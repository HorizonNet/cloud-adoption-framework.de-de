---
title: Erstellen Ihrer anfänglichen Azure-Abonnements
description: Beginnen Sie mit der Einführung von Azure, indem Sie Ihre anfänglichen Abonnements erstellen.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8a1b1838617c9d82c4e8cca239aa4abc9d853f3c
ms.sourcegitcommit: 568037e0d2996e4644c11eb61f96362a402759ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/16/2020
ms.locfileid: "84799958"
---
# <a name="create-your-initial-azure-subscriptions"></a>Erstellen Ihrer anfänglichen Azure-Abonnements

Beginnen Sie mit der Einführung von Azure, indem Sie eine erste Gruppe von Abonnements erstellen. Hier erfahren Sie, mit welchen Abonnements Sie je nach Ihren anfänglichen Anforderungen beginnen sollten.

## <a name="your-first-two-subscriptions"></a>Ihr ersten zwei Abonnements

Erstellen Sie zunächst zwei Abonnements:

- Erstellen Sie ein Azure-Abonnement, das Ihre Produktionsworkloads enthält.
- Erstellen Sie ein zweites Abonnement, das als Nichtproduktionsumgebung (Dev/Test) verwendet werden soll. Nutzen Sie dazu ein [Angebot für Azure Dev/Test](https://azure.microsoft.com/pricing/dev-test), um die Kosten niedrig zu halten.

![Ein anfängliches Abonnementmodell, das Schlüssel neben Feldern mit der Bezeichnung „Produktion“ und „Nichtproduktion“ zeigt](../../_images/ready/initial-subscription-model.png)

<!-- docsTest:ignore Dev/Test -->

Dieser Ansatz hat viele Vorteile:

- Die Verwendung separater Abonnements für Produktions- und Nichtproduktionsumgebungen schafft eine Trennung, durch die die Verwaltung Ihrer Ressourcen einfacher und sicherer wird.
- Abonnementangebote für Azure Dev/Test stehen für Nichtproduktionsworkloads zur Verfügung. Diese Angebote bieten vergünstigte Preise für Azure-Dienste und -Softwarelizenzen.
- Ihre Produktions-und Nichtproduktionsumgebungen verfügen wahrscheinlich über unterschiedliche Azure-Richtliniensätze. Mit separaten Abonnements lassen sich die verschiedenen Richtlinien ganz einfach auf Abonnementebene anwenden.
- Sie können bestimmte Azure-Ressourcentypen in Ihrem Nichtproduktionsabonnement zu Testzwecken zulassen. Diese Ressourcenanbieter können Sie in Ihrem Nichtproduktionsabonnement aktivieren, ohne sie in der Produktionsumgebung verfügbar zu machen.
- Dev/Test-Abonnements können als isolierte Sandboxumgebungen verwendet werden. Mit diesen Sandboxes können Administratoren und Entwickler schnell vollständige Sätze von Azure-Ressourcen erstellen und löschen. Diese Isolation ist auch nützlich für den Schutz und die Sicherheit von Daten.
- Wahrscheinlich definieren Sie für Produktions- und Dev/Test-Abonnements unterschiedliche akzeptable Kostenschwellenwerte.

## <a name="sandbox-subscriptions"></a>Sandboxabonnements

Wenn Innovationsziele ein Teil Ihrer Strategie für die Cloudeinführung sind, erwägen Sie die Erstellung eines oder mehrerer Sandboxabonnements. Sie können Sicherheitsrichtlinien anwenden, um diese Testabonnements von Ihren Produktions- und Nichtproduktionsumgebungen zu isolieren. In diesen isolierten Umgebungen können Benutzer problemlos mit Azure-Funktionen experimentieren. Verwenden Sie zum Erstellen dieser Abonnements ein Azure Dev/Test-Angebot.

![Ein anfängliches Abonnementmodell, das Schlüssel neben Feldern mit der Bezeichnung „Produktion“, „Nichtproduktion“ und „Sandboxes“ zeigt](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Abonnement für gemeinsam genutzte Dienste

Wenn Sie planen, **innerhalb von 24 Monaten mehr als 1.000 VMs oder Compute-Instanzen in der Cloud** zu hosten, erstellen Sie ein weiteres Azure-Abonnement für gemeinsame genutzte Dienste. So sind Sie darauf vorbereitet, Ihre endgültige Unternehmensarchitektur zu unterstützen.

![Ein anfängliches Abonnementmodell, das Schlüssel neben Feldern mit der Bezeichnung „Produktion“ und „Gemeinsam genutzte Dienste“ zeigt](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, aus welchen Gründen die [Erstellung zusätzlicher Azure-Abonnements](./scale-subscriptions.md) zum Erfüllen Ihrer Anforderungen sinnvoll sein kann.

> [!div class="nextstepaction"]
> [Erstellen zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung](./scale-subscriptions.md)
