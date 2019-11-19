---
title: Empfohlene rollenbasierte Zugriffssteuerung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Empfohlene rollenbasierte Zugriffssteuerung
author: rotycenh
ms.author: brblanch
ms.date: 11/28/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: BrianBlanchard
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 47933f12bea00ff1ea9052125147287ffc9381d6
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561775"
---
# <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

Gruppenbasierte Zugriffsrechte und Berechtigungen haben sich als eine bewährte Methode erwiesen. Der Umgang mit Gruppen anstelle von einzelnen Benutzern vereinfacht die Wartung von Zugriffsrichtlinien, bietet eine einheitliche teamübergreifende Zugriffsverwaltung und reduziert Konfigurationsfehler. Das Zuweisen und Entfernen von Benutzern zu und aus den entsprechenden Gruppen erleichtert die Aktualisierung der Berechtigungen von bestimmten Benutzern. Die [rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview) in Azure ermöglicht eine präzise Zugriffsverwaltung für Ressourcen, deren Struktur auf Benutzerrollen basiert.

Einen Überblick über die empfohlenen RBAC-Methoden als Teil einer Identitäts- und Sicherheitsstrategie finden Sie unter [Verwenden der rollenbasierten Zugriffssteuerung](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices#use-role-based-access-control).

## <a name="overview-of-role-based-access-control"></a>Übersicht über die rollenbasierte Zugriffssteuerung

Mit der [rollenbasierten Zugriffssteuerung](https://docs.microsoft.com/azure/role-based-access-control/overview) können Sie Aufgaben innerhalb Ihres Teams aufteilen und nur bestimmten Benutzern, Gruppen, Dienstprinzipalen oder verwalteten Identitäten in Azure Active Directory (Azure AD) genügend Zugriff gewähren, um ihre Aufgaben zu erfüllen. Anstatt allen uneingeschränkten Zugriff auf Ihr Azure-Abonnement oder Ihre Ressourcen zu gewähren, können Sie die Berechtigungen für jede Ressourcengruppe einschränken.

[RBAC-Rollendefinitionen](https://docs.microsoft.com/azure/role-based-access-control/role-definitions) listen Operationen auf, die für Benutzer oder Gruppen, die dieser Rolle zugeordnet sind, erlaubt oder verboten sind. Der [Bereich](https://docs.microsoft.com/azure/role-based-access-control/overview#scope) einer Rolle gibt an, auf welche Ressourcen sich diese definierten Berechtigungen beziehen. Bereiche können auf mehreren Ebenen angegeben werden: Verwaltungsgruppe, Abonnement, Ressourcengruppe oder Ressource. Bereiche sind in einer Beziehung zwischen über- und untergeordneten Elementen strukturiert.

![RBAC-Bereichshierarchie](../../_images/azure-best-practices/rbac-scope.png)

Detaillierte Anweisungen zur Zuordnung von Benutzern und Gruppen zu bestimmten Rollen und zur Zuordnung von Rollen zu Bereichen finden Sie unter [Verwalten des Zugriffs auf Azure-Ressourcen mit RBAC und dem Azure-Portal](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

Verwenden Sie bei der Planung Ihrer Zugriffssteuerungsstrategie ein Modell mit den geringsten Rechten, das den Benutzern nur die für die Ausführung ihrer Arbeit erforderlichen Berechtigungen erteilt. Die folgende Abbildung zeigt ein vorgeschlagenes Muster für die Verwendung von RBAC mit diesem Ansatz.

![Vorgeschlagenes Muster für die Verwendung von RBAC](../../_images/azure-best-practices/rbac-least-privilege.png)

> [!NOTE]
> Je spezifischer oder detaillierter die Berechtigungen sind, die Sie definieren, desto wahrscheinlicher werden Ihre Zugriffssteuerungen komplex und schwer zu verwalten sein. Dies trifft vor allem dann zu, wenn die Größe Ihrer Cloudumgebung zunimmt. Vermeiden Sie ressourcenspezifische Berechtigungen. Verwenden Sie statt dessen [Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups) für unternehmensweite Zugriffssteuerung und [Ressourcengruppen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) für Zugriffssteuerungen innerhalb von Abonnements. Vermeiden Sie auch benutzerspezifische Berechtigungen. Weisen Sie stattdessen [Gruppen in Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) Zugriffsberechtigungen zu.

## <a name="use-built-in-rbac-roles"></a>Verwenden integrierter RBAC-Rollen

Azure bietet eine Vielzahl integrierter Rollendefinitionen mit drei Kernrollen für den Zugriff:

- Die Rolle [Besitzer](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) kann alles verwalten, einschließlich des Zugriffs auf Ressourcen.
- Die Rolle [Mitwirkender](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) kann alles mit Ausnahme des Zugriffs auf Ressourcen verwalten.
- Die Rolle [Leser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader) kann alles anzeigen, aber keine Änderungen vornehmen.

Ausgehend von diesen grundlegenden Zugriffsebenen bieten zusätzliche integrierte Rollen detailliertere Steuerungsmöglichkeiten für den Zugriff auf bestimmte Ressourcentypen oder Azure-Funktionen. Beispielsweise können Sie den Zugriff auf virtuelle Computer mithilfe der folgenden integrierten Rollen verwalten:

- Mit der Rolle [Anmeldeinformationen des VM-Administrators](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-administrator-login) können Sie virtuelle Computer im Portal anzeigen und sich als _Administrator_ anmelden.
- Die Rolle [Mitwirkender für virtuelle Computer](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) ermöglicht Ihnen das Verwalten von virtuellen Computern, aber nicht den Zugriff darauf oder auf das virtuelle Netzwerk oder das Speicherkonto, mit dem sie verbunden sind.
- Die Rolle [Anmeldeinformationen für VM-Benutzer](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-user-login) kann virtuelle Computer im Portal anzeigen und sich als normaler Benutzer anmelden.

Ein weiteres Beispiel für die Verwendung integrierter Rollen zur Verwaltung des Zugriffs auf bestimmte Funktionen finden Sie in der Diskussion über die Steuerung des Zugriffs auf Kostenverfolgungsfunktionen unter [Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen oder Projekte](../azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access).

Eine Liste mit allen verfügbaren integrierten Rollen finden Sie unter [Integrierte Rollen für die rollenbasierte Zugriffssteuerung in Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).

## <a name="use-custom-roles"></a>Verwenden von benutzerdefinierten Rollen

Obwohl die integrierten Rollen in Azure eine Vielzahl von Zugriffssteuerungsszenarien unterstützen, erfüllen sie möglicherweise nicht alle Anforderungen Ihrer Organisation oder Ihres Teams. Wenn Sie beispielsweise eine einzige Gruppe von Benutzern haben, die für die Verwaltung von virtuellen Computern und Azure SQL-Datenbank-Ressourcen verantwortlich ist, können Sie eine benutzerdefinierte Rolle erstellen, um die Verwaltung der erforderlichen Zugriffssteuerungen zu optimieren.

Die Azure-RBAC-Dokumentation enthält Anweisungen zum [Erstellen benutzerdefinierter Rollen](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) sowie Details dazu, [wie Rollendefinitionen funktionieren](https://docs.microsoft.com/azure/role-based-access-control/role-definitions).

## <a name="separation-of-responsibilities-and-roles-for-large-organizations"></a>Trennung von Zuständigkeiten und Rollen für große Organisationen

RBAC ermöglicht Organisationen, verschiedene Teams für verschiedene Managementaufgaben in großen Cloudumgebungen einzusetzen. Zentralen IT-Teams kann die Steuerung der wichtigsten Zugriffs- und Sicherheitsfunktionen ermöglicht werden, während gleichzeitig Softwareentwickler und andere Teams in großem Umfang bestimmte Workloads oder Ressourcengruppen steuern können.

Die meisten Cloudumgebungen können auch von einer Zugriffssteuerungsstrategie profitieren, die mehrere Rollen verwendet und eine Trennung der Verantwortlichkeiten zwischen diesen Rollen betont. Dieser Ansatz erfordert, dass jede wesentliche Änderung an Ressourcen oder Infrastruktur mehrere Rollen betrifft, und stellt sicher, dass mehrere Personen eine Änderung überprüfen und genehmigen müssen. Diese Trennung der Verantwortlichkeiten schränkt die Fähigkeit einer einzelnen Person ein, ohne das Wissen anderer Teammitglieder auf sensible Daten zuzugreifen oder Schwachstellen einzuführen.

Die folgende Tabelle zeigt ein allgemeines Muster für die Aufteilung des IT-Zuständigkeiten in separate benutzerdefinierte Rollen:

<!-- markdownlint-disable MD033 -->

| Group | Allgemeiner Rollenname | Zuständigkeiten |
| --- | --- | --- |
| Sicherheitsvorgänge | SecOps | Bietet eine allgemeine Sicherheitsübersicht.<br/><br/> Festlegung und Durchsetzung von Sicherheitsrichtlinien wie Verschlüsselung im Ruhezustand.<br/><br/> Verwaltet Verschlüsselungsschlüssel.<br/><br/> Verwaltet Firewallregeln. |
| Netzwerkvorgänge | NetOps | Verwaltet die Netzwerkkonfiguration und den Betrieb in virtuellen Netzwerken wie Routen und Peerings. |
| Systembetrieb | SysOps | Gibt die Optionen für die Compute- und Speicherinfrastruktur an und verwaltet die bereitgestellten Ressourcen. |
| Entwicklung, Test und Betrieb | DevOps | Erstellt Workloadfunktionen und -anwendungen und stellt sie bereit.<br/><br/> Betreibt Funktionen und Anwendungen, um Vereinbarungen zum Servicelevel (Service Level Agreements, SLAs) und andere Qualitätsstandards einzuhalten. |

<!-- markdownlint-enable MD033 -->

Die Aufschlüsselung von Aktionen und Berechtigungen in diese Standardrollen ist oft für alle Ihre Anwendungen, Abonnements oder die gesamte Cloudumgebung gleich, auch wenn diese Rollen von verschiedenen Personen auf verschiedenen Ebenen ausgeführt werden. Dementsprechend können Sie einen gemeinsamen Satz von RBAC-Rollendefinitionen erstellen, die für verschiedene Bereiche innerhalb Ihrer Umgebung gelten. Benutzern und Gruppen kann dann eine gemeinsame Rolle zugewiesen werden, jedoch nur für den Bereich der Ressourcen, Ressourcengruppen, Abonnements oder Verwaltungsgruppen, für deren Verwaltung sie verantwortlich sind.

In einer [Hub-and-Spoke-Netzwerktopologie](../azure-best-practices/hub-spoke-network-topology.md) mit mehreren Abonnements könnten Sie z. B. einen gemeinsamen Satz von Rollendefinitionen für den Hub und alle Workloadspokes haben. Die NetOps-Rolle eines Hubabonnements kann Mitgliedern der zentralen IT-Abteilung der Organisation zugewiesen werden, die für die Aufrechterhaltung des Netzwerkbetriebs für gemeinsame Dienste verantwortlich sind, die von allen Workloads genutzt werden. Die NetOps-Rolle eines Workloadspokeabonnements kann dann Mitgliedern dieses spezifischen Workloadteams zugewiesen werden, sodass sie das Netzwerk innerhalb dieses Abonnements konfigurieren können, um ihre Workloadanforderungen optimal zu unterstützen. Für beide wird die gleiche Rollendefinition verwendet, aber die bereichsbasierte Zuordnungen stellen sicher, dass Benutzer nur über den Zugriff verfügen, den sie für ihre Arbeit benötigen.
