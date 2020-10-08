---
title: Bereitstellen einer CAF-Basisblaupause in Azure
description: Hier erfahren Sie, wie Sie eine CAF-Basisblaupause in Azure bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: af577cea51714b43d43d7956a69422a2316aef11
ms.sourcegitcommit: 670dd77efe02ed20275732248e0fa2aae2196805
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2020
ms.locfileid: "91621313"
---
<!-- docutune:ignore "CAF Foundation blueprint" -->

# <a name="deploy-a-caf-foundation-blueprint-in-azure"></a>Bereitstellen einer CAF-Basisblaupause in Azure

Mit der CAF-Basisblaupause wird keine Zielzone bereitgestellt. Stattdessen werden die erforderlichen Tools für ein Governance-MVP (Minimum Viable Product) bereitgestellt, um mit der Entwicklung Ihrer Governancedisziplinen zu beginnen. Diese Blaupause kann zusätzlich zu einer vorhandenen Zielzone verwendet werden und mit einer einzigen Aktion auf die Blaupause für die CAF-Migrationszielzone angewendet werden.

## <a name="deploy-the-blueprint"></a>Bereitstellen der Blaupause

Bevor Sie die CAF-Basisblaupause im Cloud Adoption Framework verwenden, machen Sie sich mit den folgenden Entwurfsprinzipien, Annahmen, Entscheidungen und Leitlinien für die Implementierung vertraut. Wenn diese Anleitung dem gewünschten Cloudeinführungsplan entspricht, kann die [CAF-Basisblaupause](/azure/governance/blueprints/samples/caf-foundation) über die Bereitstellungsschritte bereitgestellt werden.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels](/azure/governance/blueprints/samples/caf-foundation/deploy)

## <a name="design-principles"></a>Entwurfsprinzipien

Diese Implementierungsoption bietet einen wertenden Ansatz für die allgemeinen Entwurfsbereiche, die allen Azure-Zielzonen gemeinsam sind. Weitere technische Details finden Sie in den unten stehenden Annahmen und Entscheidungen.

### <a name="deployment-options"></a>Bereitstellungsoptionen

Mit dieser Implementierungsoption wird ein MVP als Grundlage für Ihre Governancedisziplinen bereitgestellt. Das Team befolgt einen modularen Refactoring-basierten Ansatz, um die Governancedisziplinen unter Verwendung der [Governancemethodik](../../govern/index.md) weiterzuentwickeln.

### <a name="enterprise-enrollment"></a>Unternehmensregistrierung

Diese Implementierungsoption nimmt hinsichtlich der Unternehmensregistrierung keine inhärente Position ein. Vielmehr ist dieser Ansatz so konzipiert, dass er unabhängig von Vertragsvereinbarungen mit Microsoft oder Microsoft-Partnern auf Kunden anwendbar ist. Vor der Bereitstellung dieser Implementierungsoption wird davon ausgegangen, dass der Kunde ein Zielabonnement erstellt hat.

### <a name="identity"></a>Identity

Bei dieser Implementierungsoption wird davon ausgegangen, dass das Zielabonnement in Einklang mit [bewährten Methoden der Identitätsverwaltung](/azure/security/fundamentals/identity-management-best-practices?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) bereits einer Azure Active Directory-Instanz zugeordnet ist.

### <a name="network-topology-and-connectivity"></a>Netzwerktopologie und -konnektivität

Bei dieser Implementierungsoption wird davon ausgegangen, dass die Zielzone bereits über eine definierte Netzwerktopologie verfügt, die den [bewährten Methoden für die Netzwerksicherheit](/azure/security/fundamentals/network-best-practices?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) entspricht.

### <a name="resource-organization"></a>Ressourcenorganisation

Mit dieser Implementierungsoption wird veranschaulicht, wie Azure Policy durch das Anwenden von Tags Elemente der Ressourcenorganisation hinzufügen kann. Konkret wird in diesem Beispiel unter Verwendung von Azure Policy ein `CostCenter`-Tag angefügt.

Das Governanceteam sollte abwägen, für welche Elemente der Ressourcenorganisation ein Tagging durchgeführt werden soll und welchen Elementen beim Abonnemententwurf Rechnung getragen wird. Diese grundlegenden Entscheidungen liefern wichtige Informationen zur Ressourcenorganisation, wenn Ihre Cloudeinführungspläne weiter fortschreiten.

Die folgenden Artikel sind für diesen frühen Vergleich bzw. diese Abwägungen innerhalb der frühen Einführungsphase hilfreich:

- [Anfängliche Azure-Abonnements](../azure-best-practices/initial-subscriptions.md): Sind in dieser Phase der Einführung zwei, drei oder vier Abonnements für Ihr Betriebsmodell erforderlich?
- [Skalieren von Abonnements](../azure-best-practices/scale-subscriptions.md): Welche Kriterien sind für eine Skalierung von Abonnements relevant, wenn die Einführung fortschreitet?
- [Organisieren von Abonnements](../azure-best-practices/organize-subscriptions.md): Wie werden Ihre Abonnements bei der Skalierung organisiert?
- [Markierungsstandards](../azure-best-practices/naming-and-tagging.md#metadata-tags): Welche weiteren Kriterien müssen einheitlich in Tags erfasst werden, um Ihren Abonnemententwurf zu erweitern?

Wenn Teams bereits weiter mit der Cloudeinführung fortgeschritten sind, finden Sie im Abschnitt zu Governancemustern im Artikel [Governanceleitfaden – Ausführlicher Leitfaden](../../govern/guides/complex/prescriptive-guidance.md#application-of-governance-defined-patterns) nützliche Informationen, die Ihnen bei diesem Vergleich bzw. bei diesen Abwägungen helfen. In diesem Abschnitt des ausführlichen Leitfadens werden eine Reihe von Mustern anhand einer bestimmten Geschichte und eines bestimmten Betriebsmodells erläutert. Darüber hinaus sind Links zu anderen Mustern enthalten, die berücksichtigt werden sollten.

### <a name="governance-disciplines"></a>Governancedisziplinen

Mit dieser Implementierung wird eine Vorgehensweise für eine ausgereifte Cost Management-Disziplin der Governancemethodik gezeigt. Dabei wird insbesondere veranschaulicht, wie Azure Policy verwendet werden kann, um eine Zulassungsliste mit bestimmten SKUs zu erstellen. Indem Sie die Typen und Größen von Ressourcen einschränken, die in einer Zielzone bereitgestellt werden können, wird das Risiko einer Budgetüberschreitung gesenkt.

Informationen zur parallelen Entwicklung der anderen Governancedisziplinen finden Sie im Abschnitt zur [Governancemethodik](../../govern/index.md). Wenn Sie die Governancedisziplin „Cost Management“ weiter verbessern möchten, finden Sie unter [Verbessern der Disziplin „Cost Management“](../../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-best-practices) weitere Informationen.

> [!WARNING]
> Mit der Weiterentwicklung der Governancedisziplinen ist möglicherweise ein Refactoring erforderlich. Möglicherweise ist ein Refactoring erforderlich. Insbesondere müssen Ressourcen später gegebenenfalls [in ein neues Abonnement oder eine neue Ressourcengruppe verschoben werden](/azure/azure-resource-manager/management/move-resource-group-and-subscription?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json).

### <a name="operations-baseline"></a>Betriebsbaseline

Bei dieser Implementierungsoption werden keine Aspekte der Betriebsbaseline implementiert. Wenn keine Betriebsbaseline definiert wurde, sollte diese Zielzone nicht für unternehmenskritische Workloads oder vertrauliche Daten verwendet werden. Es wird davon ausgegangen, dass diese Zielzone für eine eingeschränkte Produktionsbereitstellung verwendet wird, um sich parallel zu diesen anfänglichen Migrationsschritten mit dem allgemeinen Betriebsmodell vertraut zu machen und dieses weiterzuentwickeln.

Informationen zur parallelen Entwicklung einer Betriebsbaseline finden Sie im Artikel zur [Verwaltungsmethodik](../../manage/index.md). Erwägen Sie außerdem die Bereitstellung des [Azure-Serververwaltungsleitfadens](../../manage/azure-server-management/index.md).

> [!WARNING]
> Mit der Weiterentwicklung der Betriebsbaseline ist möglicherweise ein Refactoring erforderlich. Insbesondere müssen Ressourcen später gegebenenfalls [in ein neues Abonnement oder eine neue Ressourcengruppe verschoben werden](/azure/azure-resource-manager/management/move-resource-group-and-subscription?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json).

### <a name="business-continuity-and-disaster-recovery-bcdr"></a>Geschäftskontinuität und Notfallwiederherstellung (Business Continuity Disaster Recovery, BCDR)

Bei dieser Implementierungsoption wird keine BCDR-Lösung implementiert. Es wird angenommen, dass die Lösung für Schutz und Wiederherstellung durch die Entwicklung der Betriebsbaseline adressiert wird.

## <a name="assumptions"></a>Annahmen

Bei dieser anfänglichen Blaupause wird davon ausgegangen, dass das Team sich parallel zu den ersten Cloudmigrationsschritten der Ausarbeitung und Weiterentwicklung der Governancefunktionen widmet. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause verwenden, um den Vorgang zum Entwickeln einer ausgereiften Governancedisziplin zu beginnen.

- **Compliance**: In dieser Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Begrenzter Produktionsbereich:** Diese Zielzone könnte Produktionsworkloads hosten. Sie ist jedoch keine geeignete Umgebung für vertrauliche Daten oder unternehmenskritische Workloads.

Wenn diese Annahmen mit Ihren aktuellen Anforderungen in Bezug auf die Einführung übereinstimmen, ist diese Blaupause möglicherweise ein guter Ausgangspunkt zum Erstellen einer Zielzone.

## <a name="customize-or-deploy-this-blueprint"></a>Anpassen oder Bereitstellen dieser Blaupause

Erfahren Sie mehr, und laden Sie ein Referenzbeispiel der CAF-Basisblaupause für die Bereitstellung oder Anpassung der Azure-Blaupausenbeispiele herunter.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels](/azure/governance/blueprints/samples/caf-foundation/deploy)

## <a name="next-steps"></a>Nächste Schritte

Nach dem Bereitstellen Ihrer ersten Zielzone können Sie Ihre Zielzone erweitern.

> [!div class="nextstepaction"]
> [Erweitern der Zielzone](../considerations/index.md)
