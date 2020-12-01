---
title: Übertragen bestehender Azure-Umgebungen auf Unternehmensniveau
description: Integrieren vorhandener Umgebungen in eine unternehmensweite Architektur
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: csu, think-tank
ms.openlocfilehash: d97bde1bb38d9d3a0050bcbc38b99f541316c170
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447149"
---
<!-- docutune:casing resourceType resourceTypes resourceId resourceIds -->

# <a name="transition-existing-azure-environments-to-enterprise-scale"></a>Übertragen bestehender Azure-Umgebungen in eine Bereitstellung auf Unternehmensniveau

Wir sind uns bewusst, dass die meisten Organisationen über einen bestehenden Fußabdruck in Azure, ein oder mehrere Abonnements und möglicherweise eine bestehende Struktur eigener Verwaltungsgruppen verfügen. Je nach ihren anfänglichen Geschäftsanforderungen und -szenarien wurden möglicherweise Azure-Ressourcen wie z. B. hybride Konnektivität (z. B. mit Site-to-Site-VPN und/oder ExpressRoute) bereitgestellt.

Dieser Artikel hilft Organisationen, den richtigen Weg für die Übertragung bestehender Azure-Umgebung auf Unternehmensebene zu finden. In diesem Artikel werden auch Überlegungen zur Verschiebung von Ressourcen in Azure (z. B. Verschieben eines Abonnements aus einer bestehenden Verwaltungsgruppe in eine andere Verwaltungsgruppe) beschrieben, die Ihnen bei der Bewertung und Planung der Übertragung Ihrer bestehenden Azure-Umgebung in Zielzonen auf Unternehmensniveau helfen.

## <a name="moving-resources-in-azure"></a>Verschieben von Ressourcen in Azure

Einige Ressourcen in Azure können nach der Erstellung verschoben werden, und es gibt verschiedene Ansätze, die Organisationen vorbehaltlich der RBAC-Berechtigungen der Benutzer innerhalb des Geltungsbereichs und darüber hinaus verfolgen können. Die folgende Tabelle gibt einen Überblick darüber, welche Ressourcen in welchem Umfang verschoben werden können und welche Vor- und Nachteile damit verbunden sind.

| Bereich | Destination | Vorteile | Nachteile |
|--|--|--|--|
| Ressourcen in Ressourcengruppen | Können in eine neue Ressourcengruppe in demselben oder einem anderen Abonnement verschoben werden  | Ermöglicht das Ändern der Ressourcenkomposition in einer Ressourcengruppe nach der Bereitstellung | – Wird nicht von allen Ressourcentypen unterstützt <br> – Für einige Ressourcentypen gelten bestimmte Einschränkungen oder Anforderungen <br> – Die Ressourcen-IDs werden aktualisiert und wirken sich auf die vorhandene Überwachung, auf Warnungen und Vorgänge auf der Steuerungsebene aus <br> – Ressourcengruppen sind während der Dauer der Verschiebung gesperrt <br> – Erfordert die Bewertung der Richtlinien und RBAC-Vorgänge vor und nach dem Verschieben |
| Abonnements in einem Mandanten  | Können in verschiedene Verwaltungsgruppen und verschiedene Mandanten verschoben werden | Keine Auswirkung auf vorhandene Ressourcen innerhalb des Abonnements, da keine Ressourcen-ID-Werte geändert werden | Bewertung der Richtlinien und RBAC-Vorgänge vor und nach dem Verschieben erforderlich |

Um zu verstehen, welche Verschiebungsstrategie Sie verwenden sollten, werden nachfolgend Beispiele für beide Strategien erläutert:

## <a name="subscription-move"></a>Abonnementverschiebung

Häufige Anwendungsfälle für das Verschieben von Abonnements sind das Organisieren von Abonnements in Verwaltungsgruppen oder das Übertragen von Abonnements in einen neuen Azure Active Directory-Mandanten. Das Verschieben von Abonnements im Unternehmensumfang konzentriert sich auf das Verschieben von Abonnements in Verwaltungsgruppen. Das Verschieben eines Abonnements in einen neuen Mandanten dient hauptsächlich der [Übertragung des Abrechnungsbesitzes](/azure/cost-management-billing/manage/billing-subscription-transfer).

### <a name="rbac-requirements"></a>RBAC-Anforderungen

Bei der Bewertung eines Abonnements vor einer Verschiebung ist wichtig, dass der Benutzer über die erforderlichen RBAC-Berechtigungen verfügt, z. B. als Besitzer des Abonnements (direkte Rollenzuweisung), sowie über Schreibberechtigung für die Zielverwaltungsgruppe (integrierte Rollen, die dies unterstützen, sind „Besitzer“, „Mitwirkender“ und „Verwaltungsgruppenmitwirkender“).

Wenn der Benutzer die Berechtigungen der Rolle „Besitzer“ für das Abonnement von einer vorhandenen Verwaltungsgruppe geerbt hat, kann das Abonnement nur in die Verwaltungsgruppe verschoben werden, für die dem Benutzer die Rolle „Besitzer“ zugewiesen wurde.

### <a name="policy"></a>Richtlinie

Bestehende Abonnements können den Azure-Richtlinien unterliegen, die entweder direkt oder in der Verwaltungsgruppe, in der sie sich derzeit befinden, zugewiesen wurden. Es ist wichtig, die derzeitigen Richtlinien und die Richtlinien, die möglicherweise in der neuen Verwaltungsgruppe/Verwaltungsgruppenhierarchie gelten, zu bewerten.

Der Azure Resource Graph kann verwendet werden, um eine Bestandsaufnahme der vorhandenen Ressourcen durchzuführen und ihre Konfiguration mit den am Zielort vorhandenen Richtlinien zu vergleichen.

Sobald die Abonnements in eine Verwaltungsgruppe mit vorhandener RBAC und bestehenden Richtlinien verschoben wurden, sollten Sie die folgenden Optionen in Betracht ziehen:

- Die Aktualisierung der Benutzertoken im Verwaltungsgruppencache kann für jede RBAC, die an die verschobenen Abonnements vererbt wird, bis zu 30 Minuten dauern. Um diesen Vorgang zu beschleunigen, können Sie das Token aktualisieren, indem Sie sich abmelden und wieder anmelden, oder ein neues Token anfordern.
- Jede Richtlinie, bei der der Zuweisungsbereich die verschobenen Abonnements einschließt, führt Überprüfungen nur bei den vorhandenen Ressourcen durch. Dies gilt insbesondere in folgenden Fällen:
  - Jede vorhandene Ressource im Abonnement, für das die Richtlinie **deployIfNotExists** gilt, wird als nicht konform angezeigt und wird nicht automatisch korrigiert, und es ist eine Benutzerinteraktion erforderlich, um die Korrektur manuell durchzuführen.
  - Jede vorhandene Ressource im Abonnement, für das die Richtlinie **deny** gilt, wird als nicht konform angezeigt und wird nicht zurückgewiesen. Der Benutzer muss die Korrektur bei Bedarf manuell durchführen.
  - Jede vorhandene Ressource im Abonnement, für das die Richtlinien **append** und **modify** gelten, wird als nicht konform angezeigt, und es ist eine Benutzerinteraktion erforderlich, um die Korrektur durchzuführen.
  - Jede vorhandene Ressource im Abonnement, für das die Richtlinien **audit** und **auditIfNotExist** gelten, wird als nicht konform angezeigt, und es ist eine Benutzerinteraktion erforderlich, um die Korrektur durchzuführen.
- Alle neuen Schreibvorgänge für Ressourcen im verschobenen Abonnement unterliegen ganz normal den zugewiesenen Richtlinien in Echtzeit.

## <a name="resource-move"></a>Ressourcenverschiebung

Die primären Anwendungsfälle für eine Verschiebung von Ressourcen sind die Konsolidierung von Ressourcen in derselben Ressourcengruppe, wenn sie über den gleichen Lebenszyklus verfügen, oder die Verschiebung von Ressourcen in ein anderes Abonnement aufgrund von Kosten, Besitz oder RBAC-Anforderungen.

Wenn Sie eine Ressourcenverschiebung durchführen, sind sowohl die Quell- als auch die Zielressourcengruppe während des Verschiebungsvorgangs gesperrt (diese Sperre wirkt sich nicht auf die Ressourcen in der Ressourcengruppe aus), d. h. Sie können Ressourcen in den Ressourcengruppen nicht hinzufügen, aktualisieren oder löschen. Durch das Verschieben einer Ressource wird der Speicherort der Ressource nicht geändert.

### <a name="before-you-move-resources"></a>Vor dem Verschieben von Ressourcen

Vor einem Verschiebungsvorgang müssen Sie sicherstellen, dass die [Ressourcen im Bereich unterstützt werden](/azure/azure-resource-manager/management/move-support-resources) und ihre Anforderungen und Abhängigkeiten bewerten. Das Verschieben eines virtuellen Peeringnetzwerks erfordert zum Beispiel, dass Sie das Peering des virtuellen Netzwerks zunächst deaktivieren und nach Abschluss des Verschiebevorgangs wieder aktivieren. Diese Deaktivieren/Reaktivieren-Abhängigkeit erfordert die Planung im Vorfeld, um die Auswirkungen auf vorhandene Workloads zu verstehen, die mit Ihren virtuellen Netzwerken verbunden sein können.

### <a name="post-move-operation"></a>Vorgang nach dem Verschieben

Wenn die Ressourcen in eine neue Ressourcengruppe im gleichen Abonnement verschoben werden, gelten alle geerbten RBAC- und Richtlinienzuweisungen aus dem Bereich der Verwaltungsgruppe oder/und dem Abonnementbereich weiterhin. Wenn sie in eine Ressourcengruppe in einem neuen Abonnement verschoben werden, wobei das Abonnement möglicherweise anderen RBAC- und Richtlinienzuweisungen unterliegt, gelten dieselben Empfehlungen wie für das Szenario der Abonnementverschiebung, um die Ressourcenkonformität und Zugriffskontrollen zu validieren.
