---
title: Verwenden von Terraform zum Erstellen Ihrer Zielzonen
description: Erfahren Sie, wie Sie mit Terraform Ihre Zielzonen erstellen.
author: arnaudlh
ms.author: arnaul
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8eee7eeaf2406a94ee703054ed5f1b9e369bf5a2
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755655"
---
<!-- cSpell:ignore arnaudlh arnaul Arnaud vCPUs eastasia southeastasia lalogs tfvars -->

# <a name="use-terraform-to-build-your-landing-zones"></a>Verwenden von Terraform zum Erstellen Ihrer Zielzonen

Azure bietet native Dienste zum Bereitstellen Ihrer Zielzonen. Andere Tools von Drittanbietern können dabei ebenfalls helfen. Ein solches Tool, das Kunden und Partner häufig zum Bereitstellen von Zielzonen verwenden, ist Terraform von HashiCorp. In diesem Abschnitt wird gezeigt, wie Sie mit einer Beispielzielzone grundlegende Governance-, Kontoführungs- und Sicherheitsfunktionen für ein Azure-Abonnement bereitstellen.

## <a name="purpose-of-the-landing-zone"></a>Zweck der Zielzone

Die Cloud Adoption Framework-Grundlagenzielzone für Terraform bietet Features zur Durchsetzung von Protokollierung, Kontoführung und Sicherheit. Diese Zielzone verwendet als Terraform-Module bezeichnete Standardkomponenten, um die Konsistenz der in der Umgebung bereitgestellten Ressourcen zu erzwingen.

## <a name="use-standard-modules"></a>Verwenden von Standardmodulen

Die Wiederverwendung von Komponenten ist ein grundlegendes Prinzip von Infrastructure-as-Code. Die Module dienen zum Definieren von Standards und Konsistenz der gesamten Ressourcenbereitstellung inner- und außerhalb von Umgebungen. Die zum Bereitstellen dieser ersten Zielzone verwendeten Module sind in der offiziellen [Terraform-Registrierung](https://registry.terraform.io/modules/aztfmod) verfügbar.

## <a name="architecture-diagram"></a>Architekturdiagramm

In der ersten Zielzone werden die folgenden Komponenten in Ihrem Abonnement bereitgestellt:

![Grundlegende Zielzone mit Terraform](../../_images/ready/foundations-terraform-landing-zone.png)

## <a name="capabilities"></a>Funktionen

Die bereitgestellten Komponenten und ihre Zwecke sind:

<!-- markdownlint-disable MD033 -->

| Komponente | Verantwortlichkeit |
|---|---|
| Ressourcengruppen | Kernressourcengruppen, die für die Grundlage benötigt werden |
| Aktivitätsprotokollierung | Überwachung aller Abonnementaktivitäten und Archivierung: <li> Speicherkonto <li> Azure Event Hubs |
| Diagnoseprotokollierung | Alle Vorgangsprotokolle, die für eine bestimmte Anzahl von Tagen beibehalten werden: <li> Speicherkonto <li> Event Hubs |
| Log Analytics | Speichert alle Vorgangsprotokolle. Bereitstellen allgemeiner Lösungen zum umfassenden Überprüfen der bewährten Methoden von Anwendungen: <li> NetworkMonitoring <li> ADAssessment <li> ADReplication <li> AgentHealthAssessment <li> DnsAnalytics <li> KeyVaultAnalytics |
| Azure Security Center | Sicherheitsmetriken und -warnungen, die an E-Mailadressen und Telefonnummern gesendet werden |

<!-- markdownlint-enable MD033 -->

## <a name="use-this-blueprint"></a>Verwenden dieser Blaupause

Bevor Sie die grundlegende Cloud Adoption Framework-Zielzone verwenden, überprüfen Sie die folgenden Annahmen, Entscheidungen und Leitlinien für die Implementierung.

## <a name="assumptions"></a>Annahmen

Beim Definieren dieser anfänglichen Landezone wurden folgende Annahmen bzw. Einschränkungen berücksichtigt. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause zum Erstellen Ihrer ersten Landezone verwenden. Die Blaupause kann auch erweitert werden, sodass Sie eine Landezonenblaupause erstellen können, die Ihre einzigartigen Einschränkungen erfüllt.

- **Grenzwerte für Abonnements**: Bei der Einführung ist unwahrscheinlich, dass [Abonnementgrenzwerte](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) überschritten werden. Zwei allgemeine Anzeichen dafür sind eine VM-Anzahl von über 25.000 oder eine vCPU-Anzahl von über 10.000.
- **Compliance**: Für diese Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Komponenten der Architektur**: Die Komplexität der Architektur erfordert keine zusätzlichen Produktionsabonnements.
- **Gemeinsam genutzte Dienste**: Es sind keine gemeinsam genutzten Dienste in Azure vorhanden, die erfordern, dass dieses Abonnement wie ein Spoke in einer Hub-and-Spoke-Architektur behandelt wird.

Wenn diese Annahmen mit Ihrer aktuellen Umgebung übereinstimmen, kann diese Blaupause ein guter Ausgangspunkt für die Erstellung Ihrer Zielzone sein.

## <a name="design-decisions"></a>Entwurfsentscheidungen

Die folgenden Entscheidungen werden in der Terraform-Zielzone widergespiegelt:

| Komponente              | Entscheidungen                                                                                                                                                                                                                                                                | Alternative Ansätze                                                                                                                                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Protokollierung und Überwachung | Der Log Analytics-Arbeitsbereich von Azure Monitor wird verwendet. Ein Diagnosespeicherkonto und ein Event Hub werden bereitgestellt.                                                                                                                                                        |                                                                                                                                                                                                                                                                 |
| Netzwerk                | N/V: Das Netzwerk wird in einer anderen Zielzone implementiert.                                                                                                                                                                                                                    | [Netzwerkentscheidungen](../considerations/networking-options.md)                                                                                                                                                                                                 |
| Identity               | Es wird angenommen, dass das Abonnement bereits einer Azure Active Directory-Instanz zugeordnet ist.                                                                                                                                                                        | [Bewährte Methoden für die Identitätsverwaltung](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices)                                                                                                                               |
| Richtlinie                 | Bei dieser Zielzone wird derzeit davon ausgegangen, dass keine Azure-Richtlinien angewendet werden müssen.                                                                                                                                                                                            |                                                                                                                                                                                                                                                                 |
| Abonnemententwurf    | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                                                                                                                                                                                                     | [Erstellen der anfänglichen Abonnements](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                  |
| Ressourcengruppen        | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                                                                                                                                                                                                     | [Skalieren von Abonnements](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                           |
| Verwaltungsgruppen      | N/V: Wurde für ein einzelnes Produktionsabonnement entworfen.                                                                                                                                                                                                                     | [Organisieren von Abonnements](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                     |
| Daten                   | –                                                                                                                                                                                                                                                                      | [Auswählen der richtigen Bereitstellungsoption in Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) und [Auswählen des richtigen Datenspeichers](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
| Storage                | –                                                                                                                                                                                                                                                                      | [Leitfaden zu Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                  |
| Benennungsstandards       | Wenn die Umgebung erstellt wird, wird auch ein eindeutiges Präfix erstellt. Für Ressourcen, die einen global eindeutigen Namen benötigen (z. B. Speicherkonten), wird dieses Präfix verwendet. Dem benutzerdefinierten Namen wird ein zufälliges Suffix angefügt. Tags müssen wie in der folgenden Tabelle beschrieben verwendet werden. | [Best Practices zur Benennung und Kennzeichnung](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                              |
| Kostenverwaltung        | –                                                                                                                                                                                                                                                                      | [Nachverfolgen von Kosten](../azure-best-practices/track-costs.md)                                                                                                                                                                                                        |
| Compute                | –                                                                                                                                                                                                                                                                      | [Computeoptionen](../considerations/compute-options.md)                                                                                                                                                                                                         |

### <a name="tagging-standards"></a>Kennzeichnungsstandards

Bei allen Ressourcen und Ressourcengruppen müssen mindestens die folgenden Tags vorhanden sein:

| Tagname          | BESCHREIBUNG                                                                                        | Schlüssel             | Beispielwert                                    |
|-------------------|----------------------------------------------------------------------------------------------------|-----------------|--------------------------------------------------|
| Geschäftseinheit     | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. | Businessunit    | Finance, marketing, {Produktname}, corp, shared |
| Kostenstelle       | Buchhaltungskostenstelle, die dieser Ressource zugeordnet ist.                                              | Costcenter      | Number                                           |
| Notfallwiederherstellung | Geschäftliche Bedeutung der Anwendung, Workload oder dieses Diensts.                                     | Dr              | Dr-enabled, non-dr-enabled                       |
| Environment       | Bereitstellungsumgebung der Anwendung, Workload oder dieses Diensts.                                   | Env             | Prod, dev, QA, stage, test, training             |
| Name des Besitzers        | Besitzer der Anwendung, der Workload oder des Diensts.                                                    | Besitzer           | Email                                            |
| Bereitstellungstyp   | Definiert, wie die Ressourcen verwaltet werden.                                                    | Deploymenttype  | Manual, Terraform                                |
| Version           | Version der bereitgestellten Blaupause.                                                                 | Version         | V0.1                                             |
| Anwendungsname  | Der Name der Anwendung, des Diensts oder der Workload, womit die Ressource verknüpft ist.             | Applicationname | „App-Name“                                       |

<!-- cSpell:ignore caf -->

## <a name="customize-and-deploy-your-first-landing-zone"></a>Anpassen und Bereitstellen Ihrer ersten Zielzone

Sie können [Ihre grundlegende Terraform-Zielzone klonen](https://github.com/azure/caf-terraform-landingzones). Beginnen Sie einfach mit der Zielzone, indem Sie die Terraform-Variablen ändern. In unserem Beispiel wird **blueprint_foundations.sandbox.auto.tfvars** verwendet, sodass Terraform automatisch die Werte in dieser Datei für Sie festlegt.

Betrachten wir nun die verschiedenen Variablenabschnitte.

In diesem ersten Objekt erstellen wir zwei Ressourcengruppen in der `southeastasia`-Region mit den Namen `-hub-core-sec` und `-hub-operations` sowie ein Präfix, das zur Laufzeit hinzugefügt wird.

```hcl
resource_groups_hub = {
    HUB-CORE-SEC    = {
        name = "-hub-core-sec"
        location = "southeastasia"
    }
    HUB-OPERATIONS  = {
        name = "-hub-operations"
        location = "southeastasia"
    }
}
```

Als nächstes geben wir die Regionen an, in denen wir die Grundlagen festlegen können. Hier wird `southeastasia` zum Bereitstellen aller Ressourcen verwendet.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Anschließend geben wir den Aufbewahrungszeitraum für die Vorgangsprotokolle und die Protokolle des Azure-Abonnements an. Diese Daten werden in separaten Speicherkonten und einem Event Hub gespeichert, deren Namen nach dem Zufallsprinzip generiert werden, da sie eindeutig sein müssen.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

In „tags_hub“ geben wir den minimalen Satz von Tags an, die auf allen erstellten Ressourcen angewendet werden.

```hcl
tags_hub = {
    environment     = "DEV"
    owner           = "Arnaud"
    deploymentType  = "Terraform"
    costCenter      = "65182"
    BusinessUnit    = "SHARED"
    DR              = "NON-DR-ENABLED"
}
```

Anschließend geben wir den Log Analytics-Namen und eine Reihe von Lösungen an, die die Bereitstellung analysieren. Hier haben wir Netzwerküberwachung, Active Directory-Bewertung und -Replikation, DNS-Analyse und Key Vault-Analyse beibehalten.

```hcl

analytics_workspace_name = "lalogs"

solution_plan_map = {
    NetworkMonitoring = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/NetworkMonitoring"
    },
    ADAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADAssessment"
    },
    ADReplication = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADReplication"
    },
    AgentHealthAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/AgentHealthAssessment"
    },
    DnsAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/DnsAnalytics"
    },
    KeyVaultAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/KeyVaultAnalytics"
    }
}

```

Als nächstes haben wir die Warnungsparameter für Azure Security Center konfiguriert.

```hcl
# Azure Security Center Configuration
security_center = {
    contact_email   = "joe@contoso.com"
    contact_phone   = "+6500000000"
}
```

## <a name="get-started"></a>Erste Schritte

Nachdem Sie die Konfiguration überprüft haben, können Sie die Konfiguration wie eine Terraform-Umgebung bereitstellen. Sie sollten den „rover“ verwenden, einen Docker-Container, der die Bereitstellung von Windows, Linux oder macOS ermöglicht. Sie können mit den [Zielzonen](https://github.com/azure/caf-terraform-landingzones) beginnen.

## <a name="next-steps"></a>Nächste Schritte

Die grundlegende Zielzone bildet die Basis für eine aufgeschlüsselte komplexe Umgebung. Diese Edition bietet eine Reihe einfacher Funktionen, die folgendermaßen erweitert werden kann:

- Hinzufügen weiterer Module zur Blaupause.
- Überlagern mit weiteren Zielzonen.

Das Überlagern mit weiteren Zielzonen ist eine bewährte Vorgehensweise, um Systeme zu entkoppeln, jede einzelne von Ihnen verwendete Komponente zu versionieren und schnelle Innovation und Stabilität für Ihre Infrastructure-as-Code-Bereitstellung zu ermöglichen.

Zukünftige Referenzarchitekturen werden dieses Konzept für eine Hub-and-Spoke-Topologie veranschaulichen.

> [!div class="nextstepaction"]
> [Überprüfen des Beispiels der grundlegenden Terraform-Zielzone](https://github.com/azure/caf-terraform-landingzones)
