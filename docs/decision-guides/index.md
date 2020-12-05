---
title: Leitfaden zur architekturbezogenen Entscheidungsfindung
description: Verwenden Sie diese Muster und Modelle für die Kernkomponenten der Cloudbereitstellungsinfrastruktur, um Ihre spezifischen Cloudbereitstellungsszenarien zu unterstützen.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 3c0ea34fae2eb46eda498d01ed4e31e88b62df2c
ms.sourcegitcommit: d19b0fc9ef37bf1060fe7595cd2be1612a43ea4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2020
ms.locfileid: "96605454"
---
# <a name="architectural-decision-guides"></a>Leitfaden zur architekturbezogenen Entscheidungsfindung

In den Leitfäden zur architekturbezogenen Entscheidungsfindung im Framework für die Cloudeinführung werden Muster und Modelle für das Erstellen von Entwurfsanleitungen für Cloud Governance beschrieben. Jeder Leitfaden zur Entscheidungsfindung konzentriert sich auf eine zentrale Infrastrukturkomponente von Cloudbereitstellungen und führt Muster und Modelle auf, die spezifische Cloudbereitstellungsszenarien unterstützen können.

Wenn Sie beginnen, Cloud Governance in Ihrer Organisation zu etablieren, liefern nützliche Governancevorgehensweisen eine grundlegende Roadmap. Diese Anleitungen enthalten Annahmen über Anforderungen und Prioritäten, die unter Umständen nicht mit denen Ihrer Organisation übereinstimmen.

Diese Leitfäden zur Entscheidungsfindung ergänzen die exemplarischen Anleitungen zur Governance, indem sie alternative Muster und Modelle bereitstellen, die Ihnen helfen, die in der exemplarischen Entwurfsanleitung getroffenen Entscheidungen zum Architekturentwurf an Ihre eigenen Anforderungen anzupassen.

## <a name="decision-guidance-categories"></a>Kategorien von Entscheidungsleitfäden

Die folgenden Kategorien stellen grundlegende Technologien für alle Cloudbereitstellungen dar. Im Governance Journey-Beispiel werden Entwurfsentscheidungen im Zusammenhang mit diesen Technologien auf Grundlage der Anforderungen von Beispielunternehmen getroffen. Einige dieser Entscheidungen eignen sich unter Umständen nicht für die Anforderungen Ihrer Organisation. In den folgenden Abschnitten werden Alternativen für jede Kategorie erläutert, sodass Sie sich für ein Muster oder Modell entscheiden können, das besser zu Ihren individuellen Anforderungen passt.

[Abonnements](./subscriptions/index.md): Planen Sie das Abonnementmodell und die Kontenstruktur Ihrer Cloudbereitstellung entsprechend den Besitz-, Abrechnungs- und Verwaltungskonzepten Ihrer Organisation.

[Identität](./identity/index.md): Integrieren Sie cloudbasierte Identitätsdienste in Ihre vorhandenen Identitätsressourcen, um Autorisierung und Zugriffssteuerung in Ihrer IT-Umgebung zu unterstützen.

[Durchsetzung von Richtlinien](./policy-enforcement/index.md): Definieren und erzwingen Sie organisationsweite Richtlinienregeln für in der Cloud bereitgestellte Ressourcen und Workloads, die auf Ihre Governanceanforderungen ausgerichtet sind.

[Ressourcenkonsistenz](./resource-consistency/index.md): Stellen Sie sicher, dass die Bereitstellung und Organisation Ihrer cloudbasierten Ressourcen auf die Erfüllung von Ressourcenverwaltungs- und Richtlinienanforderungen ausgerichtet ist.

[Tags für Ressourcen](./resource-tagging/index.md): Strukturieren Sie Ihre cloudbasierten Ressourcen, um Abrechnungsmodelle, cloudbasierte Buchhaltungskonzepte und Verwaltungsaufgaben zu unterstützen sowie die Ressourcennutzung und die Kosten zu optimieren. Die Kategorisierung von Ressourcen erfordert ein einheitliches und überlegt organisiertes Benennungs- und Metadatendschema.

[Softwaredefiniertes Netzwerk](./software-defined-network/index.md): Stellen Sie sichere Workloads schnell in der Cloud bereit, indem Sie die Funktionen für virtualisierte Netzwerke schnell bereitstellen und modifizieren. Softwaredefinierte Netzwerke können agile Workflows unterstützen, Ressourcen isolieren und cloudbasierte Systeme in Ihre bestehende IT-Infrastruktur integrieren.

[Verschlüsselung](./encryption/index.md): Schützen Sie Ihre sensiblen Daten mittels Verschlüsselung, um den Complianceanforderungen und Sicherheitsrichtlinien Ihrer Organisation gerecht zu werden.

[Protokollierung und Berichterstellung](./logging-and-reporting/index.md): Überwachen Sie von cloudbasierten Ressourcen generierte Protokolldaten. Die Analyse von Daten liefert integritätsbezogene Erkenntnisse über den Betriebs-, Wartungs- und Compliancestatus von Workloads.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Abonnements und Konten als Grundlage einer Cloudbereitstellung dienen.

> [!div class="nextstepaction"]
> [Abonnementmodell](./subscriptions/index.md)
