---
title: Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie mehr zur Ressourcenkonsistenz bei der Planung einer Azure-Migration.
author: doodlemania2
ms.author: dermar
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 58fc2c1f3ac08fb38fcbd71e6dc1d91db768284e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221109"
---
# <a name="resource-consistency-decision-guide"></a>Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz

Das [Abonnementdesign](../subscriptions/index.md) von Azure bestimmt, wie Sie Ihre Cloudressourcen in Bezug auf die Struktur, die Buchhaltungsmethoden und die Workloadanforderungen Ihrer Organisation strukturieren. Zusätzlich zu dieser Strukturebene müssen Sie Ressourcen innerhalb eines Abonnements konsistent strukturieren, bereitstellen und verwalten können, um den organisatorischen Governance-Richtlinienanforderungen für Ihre gesamten Cloudumgebung gerecht zu werden.

![Abbildung der Konsistenzoptionen mit zunehmender Komplexität entsprechend den nachstehenden weiterführenden Links](../../_images/decision-guides/decision-guide-resource-consistency.png)

Wechseln Sie zu: [Grundlegende Gruppierung](#basic-grouping) | [Bereitstellungskonsistenz](#deployment-consistency) | [Richtlinienkonsistenz](#policy-consistency) | [Hierarchische Konsistenz](#hierarchical-consistency) | [Automatisierte Konsistenz](#automated-consistency)

Entscheidungen hinsichtlich der Konsistenzanforderungen für die Ressourcen Ihrer Cloudumgebung werden in erster Linie von folgenden Faktoren beeinflusst: Größe der digitalen Umgebung nach der Migration, geschäftliche oder umgebungsbezogene Anforderungen, die nicht exakt in Ihr bestehendes Abonnementdesign passen, sowie die Notwendigkeit einer kontinuierlichen Erzwingung von Governance, nachdem Ressourcen bereitgestellt wurden.

Mit zunehmender Bedeutung dieser Faktoren wird es auch immer wichtiger, eine konsistente Bereitstellung, Gruppierung und Verwaltung cloudbasierter Ressourcen zu gewährleisten. Um eine höhere Ressourcenkonsistenz zu erreichen und die wachsenden Anforderungen zu erfüllen, sind erhöhte Anstrengungen in den Bereichen Automatisierung, Tools und Konsistenzerzwingung erforderlich, was zu einem erhöhten Zeitaufwand für Change Management und Nachverfolgung führt.

## <a name="basic-grouping"></a>Einfache Gruppierung

In Azure sind [Ressourcengruppen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) ein zentraler Mechanismus der Ressourcenorganisation, um Ressourcen innerhalb eines Abonnements logisch zu gruppieren.

Ressourcengruppen fungieren als Container für Ressourcen mit einem gemeinsamen Lebenszyklus UND gemeinsamen Verwaltungseinschränkungen wie Richtlinien- oder RBAC-Anforderungen (Role-Based Access Control,rollenbasierte Zugriffssteuerung). Ressourcengruppen dürfen nicht geschachtelt sein, und Ressourcen dürfen nur einer einzelnen Ressourcengruppe angehören. Alle Aktionen auf der Steuerungsebene wirken sich auf alle Ressourcen in einer Ressourcengruppe aus. Beim Löschen einer Ressourcengruppe werden beispielsweise auch alle Ressourcen in dieser Gruppe entfernt. Bei der Ressourcengruppenverwaltung sollten folgende Punkte berücksichtigt werden:

1. Werden die Inhalte der Ressourcengruppe gemeinsam entwickelt?
1. Werden die Inhalte der Ressourcengruppe gemeinsam und von den gleichen Personen oder Teams verwaltet, aktualisiert und überwacht?
1. Werden die Inhalte der Ressourcengruppe gemeinsam ausgemustert?

Falls Sie eine der obigen Fragen mit _NEIN_ beantwortet haben, sollte die betreffende Ressource in einer anderen Ressourcengruppe platziert werden.

> [!IMPORTANT]
> Ressourcengruppen sind auch regionsspezifisch. Nicht selten befinden sich Ressourcen innerhalb der gleichen Ressourcengruppe jedoch in unterschiedlichen Regionen, da sie wie oben beschrieben gemeinsam verwaltet werden. Weitere Informationen zur Regionswahl finden Sie [hier](../regions/index.md).

## <a name="deployment-consistency"></a>Bereitstellungskonsistenz

Aufbauend auf dem grundlegenden Mechanismus zur Gruppierung von Ressourcen bietet die Azure-Plattform ein System zur Verwendung von Vorlagen für die Bereitstellung Ihrer Ressourcen in der Cloudumgebung. Sie können Vorlagen verwenden, um konsistente Organisations- und Benennungskonventionen bei der Bereitstellung von Workloads zu erstellen und diese Aspekte der Ressourcenbereitstellung und des Verwaltungskonzepts zu erzwingen.

[Azure Resource Manager-Vorlagen](/azure/azure-resource-manager/template-deployment-overview) ermöglichen Ihnen, Ihre Ressourcen unter Verwendung einer vorgegebenen Konfigurations- und Ressourcengruppenstruktur wiederholt in konsistentem Zustand bereitzustellen. Resource Manager-Vorlagen helfen Ihnen, eine Reihe von Standards als Grundlage für Ihre Bereitstellungen zu definieren.

Beispielsweise können Sie eine Standardvorlage für die Bereitstellung einer Webserver-Workload nutzen, die zwei virtuelle Computer als Webserver sowie einen Lastenausgleich enthält, der den Datenverkehr auf die Server verteilt. Auf der Grundlage dieser Vorlage können Sie dann jedes Mal, wenn eine solche Art von Workload benötigt wird, eine strukturell identische Gruppe mit virtuellen Computern und Lastenausgleich erstellen und müssen lediglich den Bereitstellungsnamen und die verwendeten IP-Adressen ändern.

Sie können diese Vorlagen auch programmgesteuert bereitstellen und in Ihre CI-/CD-Systeme integrieren.

## <a name="policy-consistency"></a>Richtlinienkonsistenz

Um sicherzustellen, dass Governancerichtlinien bei der Erstellung von Ressourcen befolgt werden, gehört es zum Konzept von Ressourcengruppen, beim Bereitstellen von Ressourcen eine gemeinsame Konfiguration zu verwenden.

Durch die Kombination aus Ressourcengruppen und standardisierten Resource Manager-Vorlagen können Sie Standards dahingehend erzwingen, welche Einstellungen in einer Bereitstellung erforderlich sind und welche [Azure-Richtlinienregeln](https://docs.microsoft.com/azure/governance/policy/overview) für die einzelnen Ressourcengruppen oder Ressourcen gelten sollen.

So kann es beispielsweise erforderlich sein, dass alle virtuellen Computer, die in Ihrem Abonnement bereitgestellt werden, mit einem gemeinsamen Subnetz verbunden sind, das von Ihrem zentralen IT-Team verwaltet wird. Sie können eine Standardvorlage für die Bereitstellung von Workload-VMs erstellen, um eine separate Ressourcengruppe für die Workload zu erstellen und die erforderlichen VMs in dieser bereitzustellen. Diese Ressourcengruppe weist eine Richtlinienregel auf, gemäß der nur Netzwerkschnittstellen innerhalb der Ressourcengruppe mit dem gemeinsamen Subnetz verbunden werden dürfen.

Eine ausführlichere Erläuterung der Erzwingung Ihrer Richtlinienentscheidungen innerhalb einer Cloudbereitstellung finden Sie unter [Richtlinienerzwingung](../policy-enforcement/index.md).

## <a name="hierarchical-consistency"></a>Hierarchische Konsistenz

Ressourcengruppen ermöglichen die Unterstützung zusätzlicher Hierarchieebenen Ihrer Organisation innerhalb des Abonnements. Dies wird mithilfe von Azure Policy-Regeln und Zugriffssteuerungen auf der Ressourcengruppenebene erreicht. Mit zunehmender Größe Ihrer Cloudumgebung müssen jedoch möglicherweise komplexere abonnementübergreifende Governanceanforderungen unterstützt werden als mit der Unternehmens-, Abteilungs-, Konten- und Abonnementhierarchie des Azure Enterprise Agreements möglich ist.

[Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups) ermöglichen die Einrichtung komplexerer Organisationsstrukturen für Abonnements. Hierzu werden Abonnements in einer Hierarchie gruppiert, die sich von der Enterprise Agreement-Hierarchie unterscheidet. Diese alternative Hierarchie ermöglicht die Anwendung von Zugriffssteuerungs- und Richtlinienerzwingungsmechanismen für mehrere Abonnements und die darin enthaltenen Ressourcen. Verwaltungsgruppenhierarchien können verwendet werden, um die Abonnements Ihrer Cloudumgebung auf Vorgänge oder geschäftliche Governanceanforderungen abzustimmen. Weitere Informationen finden Sie im [Leitfaden zur Entscheidungsfindung für Abonnements](../subscriptions/index.md).

## <a name="automated-consistency"></a>Automatisierte Konsistenz

Bei großen Cloudbereitstellungen wird globale Governance immer wichtiger und komplexer. Es ist von entscheidender Bedeutung, auf Governance bezogene Vorgaben bei der Bereitstellung von Ressourcen automatisch um- und durchzusetzen sowie aktualisierte Anforderungen für bestehende Bereitstellungen zu erfüllen.

[Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) ermöglichen Organisationen das Unterstützen globaler Governance in großen Cloudumgebungen in Azure. Diese Blaupausen gehen über die von den Standardvorlagen von Azure Resource Manager bereitgestellten Funktionen hinaus und dienen zum Erstellen kompletter Bereitstellungsorchestrierungen, die in der Lage sind, Ressourcen bereitzustellen und Richtlinienregeln zu befolgen. Die Blaupausen unterstützen die Versionsverwaltung, die Möglichkeit, alle Abonnements zu aktualisieren, in denen eine Blaupause verwendet wurde, und die Möglichkeit, bereitgestellte Abonnements zu sperren, um die unbefugte Erstellung und Änderung von Ressourcen zu verhindern.

Diese Bereitstellungspakete ermöglichen IT- und Entwicklungsteams, schnell neue Workloads und Netzwerkressourcen bereitzustellen, die den sich ändernden Anforderungen von Unternehmensrichtlinien entsprechen. Blaupausen können auch in CI-/CD-Pipelines integriert werden, um überarbeitete Governancestandards auf Bereitstellungen anzuwenden, sobald diese aktualisiert werden.

## <a name="next-steps"></a>Nächste Schritte

„Ressourcenkonsistenz“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
