---
title: Erstellen zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie eine Strategie für die Skalierung Ihrer Umgebung mit mehreren Azure-Abonnements entwickeln.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ec2cac2978047a95ef2199933286ec98e2e6d63f
ms.sourcegitcommit: 71a4f33546443d8c875265ac8fbaf3ab24ae8ab4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86479839"
---
# <a name="create-additional-subscriptions-to-scale-your-azure-environment"></a>Erstellen zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung

Organisationen verwenden häufig mehrere Azure-Abonnements, um die pro Abonnement geltenden Ressourceneinschränkungen zu vermeiden und ihre Azure-Ressourcen besser verwalten und steuern zu können. Es ist wichtig, dass Sie eine Strategie für die Skalierung Ihrer Abonnements definieren.

## <a name="review-fundamental-concepts"></a>Verständnis der grundlegenden Konzepte

Wenn Sie Ihre Azure-Umgebung über Ihre [anfänglichen Abonnements](./initial-subscriptions.md) hinaus erweitern, ist es wichtig, sich mit Azure-Konzepten wie Konten, Mandanten, Verzeichnissen und Abonnements vertraut zu machen. Weitere Informationen finden Sie unter [Grundlegende Konzepte in Azure](../considerations/fundamental-concepts.md).

Weitere Faktoren und Überlegungen können zusätzliche Abonnements erforderlich machen. Beachten Sie Folgendes, wenn Sie Ihre Cloudumgebung erweitern.

## <a name="technical-considerations"></a>Technische Überlegungen

**Grenzwerte für Abonnements**: Bei Abonnements gelten für einige Ressourcentypen bestimmte Grenzwerte. Beispielsweise ist die Anzahl von virtuellen Netzwerken in einem Abonnement begrenzt. Wenn ein Abonnement diese Grenzwerte erreicht, müssen Sie ein weiteres Abonnement erstellen und ihm zusätzliche Ressourcen zuordnen. Weitere Informationen finden Sie unter [Einschränkungen für Azure-Abonnements und Dienste, Kontingente und Einschränkungen](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#general-limits).

**Ressourcen des klassischen Modells:** Wenn Sie Azure schon lange nutzen, haben Sie möglicherweise Ressourcen, die mit dem klassischen Bereitstellungsmodell erstellt wurden. Azure-Richtlinien, rollenbasierte Zugriffssteuerung, Ressourcengruppierung und -tags können nicht auf Ressourcen des klassischen Modells angewendet werden. Sie sollten diese Ressourcen in Abonnements verschieben, die nur Ressourcen des klassischen Modells enthalten.

**Kosten:** Möglicherweise fallen zusätzliche Kosten für Dateneingang und -ausgang zwischen Abonnements an.

## <a name="business-priorities"></a>Geschäftliche Prioritäten

Möglicherweise veranlassen Ihre geschäftlichen Prioritäten Sie, zusätzliche Abonnements zu erstellen. Dazu zählen folgende Prioritäten:

- Innovation
- Migration
- Kosten
- Operationen (Operations)
- Sicherheit
- Governance

Weitere Überlegungen zum Skalieren Ihrer Abonnements finden Sie im [Leitfaden zur Entscheidungsfindung für Abonnements](../../decision-guides/subscriptions/index.md) im Cloud Adoption Framework.

## <a name="moving-resources-between-subscriptions"></a>Verschieben von Ressourcen zwischen Abonnements

Wenn Ihr Abonnementmodell wächst, entscheiden Sie vielleicht, dass einige Ressourcen in andere Abonnements gehören. Viele Ressourcentypen können zwischen Abonnements verschoben werden. Sie können auch automatisierte Bereitstellungen verwenden, um Ressourcen in einem anderen Abonnement neu zu erstellen. Weitere Informationen finden Sie unter [Verschieben von Azure-Ressourcen in eine andere Ressourcengruppe oder ein anderes Abonnement](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription).

## <a name="tips-for-creating-new-subscriptions"></a>Tipps zum Erstellen neuer Abonnements

- Bestimmen Sie, wer für das Erstellen neuer Abonnements zuständig sein soll.
- Entscheiden Sie, welche Ressourcentypen standardmäßig in einem Abonnement enthalten sein sollen.
- Entscheiden Sie, wie alle Standardabonnements aussehen sollen. Zu den Überlegungen zählen RBAC-Zugriff, Richtlinien, Tags und Infrastrukturressourcen.
- Wenn möglich, [erstellen Sie neue Abonnements programmgesteuert](https://docs.microsoft.com/azure/azure-resource-manager/management/programmatically-create-subscription) über einen Dienstprinzipal. Sie müssen [dem Dienstprinzipal die Berechtigung erteilen](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription), Abonnements zu erstellen. Definieren Sie eine Sicherheitsgruppe, die neue Abonnements über einen automatisierten Workflow anfordern kann.
- Wenn Sie ES-Kunde (Enterprise Agreement) sind, bitten Sie den Azure-Support, die Erstellung von Nicht-EA-Abonnements für Ihre Organisation zu sperren.

## <a name="next-steps"></a>Nächste Schritte

Erstellen Sie eine Verwaltungsgruppenhierarchie, um [Ihre Abonnements und Ressourcen zu organisieren und zu verwalten](./organize-subscriptions.md).

> [!div class="nextstepaction"]
> [Organisieren und Verwalten Ihrer Abonnements und Ressourcen](./organize-subscriptions.md)
