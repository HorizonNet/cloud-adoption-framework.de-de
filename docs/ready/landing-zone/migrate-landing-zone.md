---
title: Bereitstellen einer Landezone in Azure
description: Erfahren Sie, wie Sie in Azure eine Landezone für die Migration bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 3777dd0cfebba040dd42db3229a925856971947e
ms.sourcegitcommit: 78fa714f964225cd5fc7a762e83fafe9b3f9dea1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89427823"
---
# <a name="deploy-a-migration-landing-zone-in-azure"></a>Bereitstellen einer Landezone in Azure

Die Zielzone für die Migration ist eine Umgebung, die bereitgestellt und auf das Hosten von Workloads vorbereitet wurde, die von einer lokalen Umgebung nach Azure migriert werden.

## <a name="deploy-the-blueprint"></a>Bereitstellen der Blaupause

Bevor Sie die CAF-Migrationszielzonen-Blaupause im Cloud Adoption Framework verwenden, machen Sie sich mit den folgenden Entwurfsprinzipien, Annahmen, Entscheidungen und Leitlinien für die Implementierung vertraut. Wenn diese Anleitung dem gewünschten Cloudeinführungsplan entspricht, kann die [CAF-Migrationszielzonen-Blaupause](/azure/governance/blueprints/samples/caf-migrate-landing-zone) mithilfe der Bereitstellungsschritte bereitgestellt werden.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels](/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy)

## <a name="design-principles"></a>Entwurfsprinzipien

Diese Implementierungsoption bietet einen wertenden Ansatz für die allgemeinen Entwurfsbereiche, die allen Azure-Zielzonen gemeinsam sind. Weitere technische Details finden Sie in den Annahmen und Entscheidungen unten.

### <a name="deployment-options"></a>Bereitstellungsoptionen

Mit dieser Implementierungsoption wird ein Minimum Viable Product (MVP) bereitgestellt, um eine Migration zu starten. Im Verlauf der Migration verfolgt der Kunde bei paralleler Anleitung einen modularen Umgestaltungsansatz zum Ausbau des Betriebsmodells; hierbei kommen die [Governancemethodik](../../govern/index.md) und die [Manage-Methodik](../../manage/index.md) zur Anwendung, um die komplexen Themen parallel zu den anfänglichen Migrationsmaßnahmen zu adressieren.

Die von diesem MVP-Ansatz bereitgestellten spezifischen Ressourcen werden unten im Abschnitt zu [Entscheidungen](#decisions) aufgeführt.

### <a name="enterprise-enrollment"></a>Unternehmensregistrierung

Diese Implementierungsoption nimmt hinsichtlich der Unternehmensregistrierung keine inhärente Position ein. Dieser Ansatz ist so konzipiert, dass er unabhängig von Vertragsvereinbarungen mit Microsoft oder Microsoft-Partnern auf Kunden anwendbar ist. Es wird angenommen, dass der Kunde vor der Bereitstellung dieser Implementierungsoption ein Zielabonnement erstellt hat.

### <a name="identity"></a>Identity

Bei dieser Implementierungsoption wird davon ausgegangen, dass das Zielabonnement in Einklang mit [bewährten Methoden der Identitätsverwaltung](/azure/security/fundamentals/identity-management-best-practices?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) bereits einer Azure Active Directory-Instanz zugeordnet ist.

### <a name="network-topology-and-connectivity"></a>Netzwerktopologie und -konnektivität

Bei dieser Implementierungsoption wird ein virtuelles Netzwerk mit Subnetzen für Gateway, Firewall, Jumpbox und Zielzone erstellt. In der nächsten Iteration befolgt das Team den [Leitfaden für Entscheidungen zum Netzwerkentwurf](../considerations/networking-options.md), um in Einklang mit [bewährten Methoden der Netzwerksicherheit](/azure/security/fundamentals/network-best-practices?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) die geeignete Form von Konnektivität zwischen dem Gatewaysubnetz und anderen Netzwerken zu implementieren.

### <a name="resource-organization"></a>Ressourcenorganisation

Bei dieser Implementierungsoption wird eine einzelne Zielzone erstellt, in der Ressourcen in Workloads organisiert sind, die durch spezifische Ressourcengruppen definiert sind. Durch die Auswahl dieses minimalistischen Ansatzes für die Ressourcenorganisation werden die technischen Entscheidungen der Ressourcenorganisation auf einen Zeitpunkt verschoben, zu dem Cloudbetriebsmodell des Teams eindeutiger definiert ist.

Dieser Ansatz beruht auf der Annahme, dass die Cloudeinführungsmaßnahmen die [Abonnementgrenzen](/azure/azure-resource-manager/management/azure-subscription-service-limits) nicht überschreiten. Diese Option setzt auch begrenzte architekturbezogene Komplexitäts- und Sicherheitsanforderungen in dieser Zielzone voraus.

Sollte sich dies im Rahmen des Cloudeinführungsplans ändern, muss die Ressourcenorganisation u. U. anhand der Anleitung in der [Governancemethodik](../../govern/index.md) umgestaltet werden.

### <a name="governance-disciplines"></a>Disziplinen der Governance

Bei dieser Implementierungsoption werden keine Governancetools implementiert. Bei fehlender definierter Richtlinienautomatisierung sollte diese Zielzone nicht für unternehmenskritische Workloads oder vertrauliche Daten verwendet werden. Es wird davon ausgegangen, dass diese Zielzone für eine begrenzte Produktionsbereitstellung verwendet wird, um Lern-, Iterations- und Entwicklungszwecke des allgemeinen Betriebsmodells parallel zu diesen frühen Phasen der Migration zu initiieren.

Um die parallele Entwicklung von Disziplinen der Governance zu beschleunigen, sehen Sie sich die [Governancemethodik](../../govern/index.md) an, und überlegen Sie, ob Sie zusätzlich zur Blaupause für die CAF-Migrationszielzone die [Blaupause für CAF-Grundlagen](./foundation-blueprint.md) bereitstellen möchten.

> [!WARNING]
> Mit der Weiterentwicklung der Disziplinen der Governance ist möglicherweise eine Umgestaltung erforderlich. Insbesondere müssen später Ressourcen [in ein neues Abonnement oder eine neue Ressourcengruppe verschoben werden](/azure/azure-resource-manager/management/move-resource-group-and-subscription?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json).

### <a name="operations-baseline"></a>Betriebsbaseline

Bei dieser Implementierungsoption werden keine Vorgänge implementiert. Bei fehlender definierter Betriebsbaseline sollte diese Zielzone nicht für unternehmenskritische Workloads oder vertrauliche Daten verwendet werden. Es wird davon ausgegangen, dass diese Zielzone für eine begrenzte Produktionsbereitstellung verwendet wird, um Lern-, Iterations- und Entwicklungszwecke des allgemeinen Betriebsmodells parallel zu diesen frühen Phasen der Migration zu initiieren.

Wenn Sie die parallele Entwicklung einer Betriebsbaseline beschleunigen möchten, sehen Sie sich die [Manage-Methodik](../../manage/index.md) an, und überlegen Sie, ob Sie den [Azure-Serververwaltungsleitfaden](../../manage/azure-server-management/index.md) bereitstellen möchten.

> [!WARNING]
> Mit der Weiterentwicklung der Betriebsbaseline ist möglicherweise eine Umgestaltung erforderlich. Insbesondere müssen später Ressourcen [in ein neues Abonnement oder eine neue Ressourcengruppe verschoben werden](/azure/azure-resource-manager/management/move-resource-group-and-subscription?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json).

### <a name="business-continuity-and-disaster-recovery-bcdr"></a>Geschäftskontinuität und Notfallwiederherstellung (Business Continuity Disaster Recovery, BCDR)

Bei dieser Implementierungsoption wird keine BCDR-Lösung implementiert. Es wird angenommen, dass die Lösung für Schutz und Wiederherstellung durch die Entwicklung der Betriebsbaseline adressiert wird.

## <a name="assumptions"></a>Annahmen

Diese anfängliche Zielzone umfasst folgende Annahmen bzw. Einschränkungen. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause zum Erstellen Ihrer ersten Landezone verwenden. Die Blaupause kann auch erweitert werden, sodass Sie eine Landezonenblaupause erstellen können, die Ihre einzigartigen Einschränkungen erfüllt.

- **Grenzwerte für Abonnements**: Bei der Einführung ist nicht damit zu rechnen, dass [Abonnementgrenzwerte](/azure/azure-resource-manager/management/azure-subscription-service-limits) überschritten werden.
- **Compliance**: In dieser Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Komponenten der Architektur**: Die Komplexität der Architektur erfordert keine zusätzlichen Produktionsabonnements.
- **Gemeinsam genutzte Dienste**: Keiner der vorhandenen gemeinsam genutzten Dienste in Azure erfordert, dass dieses Abonnement wie ein Spoke in einer Hub-and-Spoke-Architektur behandelt wird.
- **Begrenzter Produktionsbereich:** Diese Zielzone könnte Produktionsworkloads hosten. Sie ist jedoch keine geeignete Umgebung für vertrauliche Daten oder unternehmenskritische Workloads.

Wenn diese Annahmen mit Ihren aktuellen Anforderungen in Bezug auf die Einführung übereinstimmen, ist diese Blaupause möglicherweise ein guter Ausgangspunkt zum Erstellen einer Zielzone.

## <a name="decisions"></a>Entscheidungen

Die folgenden Entscheidungen werden in der Blaupause für die Landezone widergespiegelt.

| Komponente                    | Entscheidungen                                                                                         | Alternative Ansätze                                                                                                                                                                                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Migrationstools              | Azure Site Recovery wird bereitgestellt, und ein Azure Migrate-Projekt wird erstellt.                | [Entscheidungsleitfaden zur Wahl von Migrationstools](../../decision-guides/migrate-decision-guide/index.md)                                                                                                                                                                                               |
| Protokollierung und Überwachung       | Ein Operational Insights-Arbeitsbereich und ein Speicherkonto für die Diagnose werden bereitgestellt.                |                                                                                                                                                                                                                                                                                       |
| Netzwerk                      | Es wird ein virtuelles Netzwerk mit Subnetzen für Gateway, Firewall, Jumpbox und Landezone erstellt.  | [Netzwerkentscheidungen](../considerations/networking-options.md)                                                                                                                                                                                                                       |
| Identity                     | Es wird angenommen, dass das Abonnement bereits einer Azure Active Directory-Instanz zugeordnet ist. | [Bewährte Methoden für die Identitätsverwaltung](/azure/security/fundamentals/identity-management-best-practices?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) |
| Richtlinie                       | Bei dieser Blaupause wird derzeit davon ausgegangen, dass keine Azure-Richtlinien angewendet werden müssen.                        |                                                                                                                                                                                                                                                                                       |
| Abonnemententwurf          | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Erstellen der anfänglichen Abonnements](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                                      |
| Ressourcengruppen              | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Skalieren von Abonnements](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                                                 |
| Verwaltungsgruppen            | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Organisieren und Verwalten von Abonnements](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                                |
| Daten                         | –                                                                                               | [Auswählen der richtigen Bereitstellungsoption in Azure SQL](/azure/sql-database/sql-database-paas-vs-sql-server-iaas) und [Auswählen des richtigen Datenspeichers](/azure/architecture/guide/technology-choices/data-store-overview)                       |
| Storage                      | –                                                                                               | [Leitfaden zu Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                                        |
| Standards für Benennung und Kennzeichnung | –                                                                                               | [Best Practices zur Benennung und Kennzeichnung](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                                                    |
| Kostenverwaltung              | –                                                                                               | [Nachverfolgen von Kosten](../azure-best-practices/track-costs.md)                                                                                                                                                                                                                              |
| Compute                      | –                                                                                               | [Computeoptionen](../considerations/compute-options.md)                                                                                                                                                                                                                               |

## <a name="customize-or-deploy-a-landing-zone"></a>Anpassen oder Bereitstellen einer Zielzone

Erfahren Sie mehr, und laden Sie ein Referenzbeispiel der CAF-Migrationszielzonen-Blaupause für die Bereitstellung oder Anpassung von den Azure-Blaupausenbeispielen herunter.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels](/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy)

Eine Anleitung zu den Anpassungen, die in dieser Blaupause oder der resultierenden Zielzone vorgenommen werden sollten, finden Sie in den [Überlegungen zu Zielzonen](../considerations/index.md).

## <a name="next-steps"></a>Nächste Schritte

Nach dem Bereitstellen Ihrer ersten Zielzone können Sie Ihre Zielzone erweitern.

> [!div class="nextstepaction"]
> [Erweitern der Zielzone](../considerations/index.md)
