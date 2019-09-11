---
title: Migrationsumgebung – Planungscheckliste
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Überprüfen der Umgebungsbereitschaft vor der Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8d216d65685c7e58fc622a5d7f820f0c23097fa4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839028"
---
# <a name="migration-environment-planning-checklist---validate-environmental-readiness-prior-to-migration"></a>Planungscheckliste für die Migrationsumgebung – Überprüfen der Umgebungsbereitschaft vor der Migration

Als einen ersten Schritt im Migrationsprozess müssen Sie die richtige Umgebung in der Cloud erstellen, um migrierte Ressourcen empfangen, hosten und unterstützen zu können. Dieser Artikel enthält eine Liste der Dinge, die Sie vor der Migration in der aktuellen Umgebung überprüfen müssen.

Die folgende Checkliste entspricht den Anweisungen im Abschnitt [Bereit](../../../ready/index.md) des Framework für die Cloudeinführung. Lesen Sie diesen Abschnitt, um Hinweise zur Ausführung eines der folgenden Punkte zu erhalten.

## <a name="effort-type-assumption"></a>Annahme zum Aufwandstyp

Bei diesem Artikel und der Checkliste wird von einem Ansatz des Typs _Zuweisen eines neuen Hosts_ oder _Übergang in die Cloud_ für die Cloudmigration ausgegangen.

## <a name="governance-alignment"></a>Governanceausrichtung

Die erste und wichtigste Entscheidung in Bezug auf eine migrationsbereite Umgebung ist die Auswahl der Governanceausrichtung. Wurde ein Konsens über die Ausrichtung von Governance und Migrationsgrundlage erzielt? Dem Cloudeinführungsteam sollte mindestens bekannt sein, ob diese Migration eine einzelne Umgebung mit begrenzter Governance, eine vollständig gesteuerte Umgebungsfactory oder eine Variante dazwischen zum Ziel hat. Weitere Optionen und Anleitungen zur Governanceausrichtung finden Sie im Artikel zu [Governance- und Complianceausrichtung](../../expanded-scope/governance-or-compliance.md).

## <a name="cloud-readiness-implementation"></a>Implementierung der Cloudbereitschaft

Unabhängig davon, ob Sie sich bei Ihrer ersten Migration für eine umfassendere Cloud-Governance-Strategie entscheiden oder nicht, müssen Sie sicherstellen, dass Ihre Cloudbereitstellungsumgebung für die Unterstützung Ihrer Workloads konfiguriert ist.

Wenn Sie planen, die Migration von Anfang an auf eine Cloud-Governance-Strategie auszurichten, müssen Sie die [Fünf Disziplinen der Cloud Governance](../../../governance/governance-disciplines.md) anwenden, um auf Informationen basierende Entscheidungen zu Richtlinien, Toolketten und Erzwingungsmechanismen treffen zu können, mit denen Ihre Cloudumgebung an die allgemeinen Unternehmensanforderungen angepasst wird. In den [Governance-Entwurfshandbüchern](../../../governance/journeys/index.md) des Framework für die Cloudeinführung finden Sie Beispiele dafür, wie dieses Modell mit Azure-Diensten implementiert wird.

Wenn Ihre anfänglichen Migrationen nicht eng mit einer umfassenderen Cloud-Governance-Strategie verbunden sind, müssen noch die allgemeinen Fragen der Organisations-, Zugriffs- und Infrastrukturplanung geklärt werden. Unterstützung bei diesen Entscheidungen für die Cloudbereitschaft finden Sie im [Leitfaden für die Azure-Bereitschaft](../../../ready/azure-readiness-guide/index.md).

> [!CAUTION]
> Es wird dringend empfohlen, eine Governancestrategie für alles zu entwickeln, was über die anfängliche Workloadmigration hinausgeht.

Unabhängig vom Grad Ihrer Governanceausrichtung müssen Sie Entscheidungen zu den folgenden Themen treffen.

### <a name="resource-organization"></a>Ressourcenorganisation

Basierend auf der Entscheidung zur Governanceausrichtung sollte vor der Migration ein Ansatz für die Organisation und Bereitstellung von Ressourcen festgelegt werden.

### <a name="nomenclature"></a>Benennung

Vor der Migration sollten ein einheitlicher Ansatz für die Benennung von Ressourcen sowie konsistente Benennungsschemas festgelegt werden.

### <a name="resource-governance"></a>Ressourcenkontrolle

Vor der Migration sollte eine Entscheidung über die Tools zur Ressourcenverwaltung getroffen werden. Die Tools müssen nicht vollständig implementiert sein, doch sollte eine Richtung ausgewählt und getestet sein. Es wird empfohlen, dass das Cloudgovernanceteam vor der Migration die Implementierung eines Minimum Viable Product (MVP) für Governancetools definiert und anfordert.

## <a name="network"></a>Netzwerk

Ihre cloudbasierten Workloads erfordern die Bereitstellung virtueller Netzwerke zur Unterstützung des Endbenutzer- und Administratorzugriffs. Basierend auf Entscheidungen zur Ressourcenorganisation und Ressourcenkontrolle sollten Sie einen Netzwerkansatz wählen, der sich an den Anforderungen der IT-Sicherheit orientiert. Darüber hinaus sollten Ihre Netzwerkentscheidungen auf alle Einschränkungen des Hybridnetzwerks abgestimmt sein, die für den Betrieb der Workloads im Migrationsbacklog und zur Unterstützung des Zugriffs auf lokal gehostete Ressourcen erforderlich sind.

## <a name="identity"></a>Identity

Cloudbasierte Identitätsdienste sind eine Voraussetzung für das Anbieten von Identitäts- und Zugriffsverwaltung (IAM) für Ihre Cloudressourcen. Stimmen Sie Ihre Identitätsverwaltungsstrategie auf Ihre Cloudeinführungspläne ab, bevor Sie fortfahren. Ziehen Sie beispielsweise bei der Migration vorhandener lokaler Ressourcen die Unterstützung eines Hybrididentitätsansatzes mithilfe einer [Verzeichnissynchronisierung](../../../decision-guides/identity/index.md) in Betracht, um einen konsistenten Satz von Benutzeranmeldeinformationen in Ihrer lokalen Umgebung und Cloudumgebung während und nach der Migration zu ermöglichen.

## <a name="next-steps"></a>Nächste Schritte

Wenn die Umgebung die Mindestanforderungen erfüllt, kann sie als genehmigt für die Migrationsbereitschaft betrachtet werden. [Kulturelle Komplexität und Change Management](./culture-complexity.md) hilft, Rollen und Verantwortlichkeiten aufeinander abzustimmen, um entsprechende Erwartungen während der Ausführung des Plans sicherzustellen.

> [!div class="nextstepaction"]
> [Kulturelle Komplexität und Change Management](./culture-complexity.md)
