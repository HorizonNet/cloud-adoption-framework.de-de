---
title: Verwenden von Terraform zum Erstellen Ihrer Zielzonen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie mit Terraform Ihre Zielzonen erstellen.
author: arnaudlh
ms.author: arnaul
ms.date: 10/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 51751ab0033505e34c02c17db363bc985b83e44d
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058154"
---
# <a name="use-terraform-to-build-your-landing-zones"></a>Verwenden von Terraform zum Erstellen Ihrer Zielzonen

Azure bietet native Dienste zum Bereitstellen Ihrer Zielzonen. Andere Tools von Drittanbietern können dabei ebenfalls helfen. Ein solches Tool, das Kunden und Partner häufig zum Bereitstellen von Zielzonen verwenden, ist Terraform von Hashicorp. In diesem Abschnitt wird gezeigt, wie Sie mit einer Prototypzielzone grundlegende Protokollierungs-, Kontoführungs- und Sicherheitsfunktionen für ein Azure-Abonnement bereitstellen.

## <a name="purpose-of-the-landing-zone"></a>Zweck der Zielzone

Die grundlegende Zielzone von Cloud Adoption Framework für Terraform verfügt über eine begrenzte Anzahl von Zuständigkeiten und Features zum Erzwingen von Protokollierung, Kontoführung und Sicherheit. Wir haben diese Zielzone so entworfen, dass als Terraform-Module bezeichnete Standardkomponenten verwendet werden, um die Konsistenz der in der Umgebung bereitgestellten Ressourcen zu erzwingen.

## <a name="using-standard-modules"></a>Verwenden von Standardmodulen

Die Wiederverwendung von Komponenten ist ein grundlegendes Prinzip von Infrastructure-as-Code. Die Module dienen zum Definieren von Standards und Konsistenz der gesamten Ressourcenbereitstellung inner- und außerhalb von Umgebungen. Der Satz von Modulen zum Bereitstellen dieser ersten Zielzone ist in der offiziellen [Terraform-Registrierung](https://registry.terraform.io/search?q=aztfmod) verfügbar.

## <a name="architecture-diagram"></a>Architekturdiagramm

In der ersten Zielzone werden die folgenden Komponenten in Ihrem Abonnement bereitgestellt:

![Grundlegende Zielzone mit Terraform](../../_images/ready/foundations-terraform-landingzone.png)

## <a name="capabilities"></a>Funktionen

Die bereitgestellten Komponenten und ihre Zwecke sind:

| Komponente | Verantwortlichkeit |
|---------|---------|
| Ressourcengruppen | Kernressourcengruppen, die für die Grundlage benötigt werden |
| Aktivitätsprotokollierung | Überwachung aller Abonnementaktivitäten und Archivierung: </br> – Speicherkonto </br> – Event Hubs |  
| Diagnoseprotokollierung | Alle Vorgangsprotokolle, die für eine bestimmte Anzahl von Tagen beibehalten werden: </br> – Speicherkonto </br> – Event Hubs |
| Log Analytics | Speichert alle Vorgangsprotokolle </br> Bereitstellen allgemeiner Lösungen zum umfassenden Überprüfen der bewährten Methoden von Anwendungen: </br> – NetworkMonitoring </br> – ADAssessment </br> – ADReplication </br> – Agenthalthassessment </br> – DnsAnalytics </br> – KeyVaultAnalytics
| Security Center | Sicherheitsmetriken und -warnungen, die an E-Mailadressen und Telefonnummern gesendet werden |

## <a name="use-this-blueprint"></a>Verwenden dieser Blaupause

Bevor Sie die grundlegende Cloud Adoption Framework-Zielzone verwenden, überprüfen Sie die folgenden Annahmen, Entscheidungen und Leitlinien für die Implementierung.

## <a name="assumptions"></a>Annahmen

Beim Definieren dieser anfänglichen Landezone wurden folgende Annahmen bzw. Einschränkungen berücksichtigt. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause zum Erstellen Ihrer ersten Landezone verwenden. Die Blaupause kann auch erweitert werden, sodass Sie eine Landezonenblaupause erstellen können, die Ihre einzigartigen Einschränkungen erfüllt.

- **Grenzwerte für Abonnements**: Bei der Einführung ist unwahrscheinlich, dass [Abonnementgrenzwerte](https://docs.microsoft.com/azure/azure-subscription-service-limits) überschritten werden. Zwei allgemeine Anzeichen dafür sind eine VM-Anzahl von über 25.000 oder eine vCPU-Anzahl von über 10.000.
- **Compliance**: Für diese Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Komponenten der Architektur**: Die Komplexität der Architektur erfordert keine zusätzlichen Produktionsabonnements.
- **Gemeinsam genutzte Dienste**: Es sind keine gemeinsam genutzten Dienste in Azure vorhanden, die erfordern, dass dieses Abonnement wie ein Spoke in einer Hub-and-Spoke-Architektur behandelt wird.

Wenn diese Annahmen mit Ihrer aktuellen Umgebung übereinstimmen, kann diese Blaupause ein guter Ausgangspunkt für die Erstellung Ihrer Zielzone sein.

## <a name="design-decisions"></a>Entwurfsentscheidungen

Die folgenden Entscheidungen werden in der Terraform-Zielzone widergespiegelt:

| Komponente | Entscheidungen | Alternative Ansätze |
| --- | --- | --- |
|Protokollierung und Überwachung | Ein Azure Monitor Log Analytics-Arbeitsbereich wird verwendet. Ein Diagnosespeicherkonto und ein Event Hub werden bereitgestellt. |         |
|Netzwerk | Nicht verfügbar: Das Netzwerk wird in einer anderen Zielzone implementiert. |[Netzwerkentscheidungen](../considerations/network-decisions.md) |
|Identity | Es wird angenommen, dass das Abonnement bereits einer Azure Active Directory-Instanz zugeordnet ist. | [Bewährte Methoden für die Identitätsverwaltung](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) |
| Richtlinie | Bei dieser Zielzone wird derzeit davon ausgegangen, dass keine Azure-Richtlinien angewendet werden müssen. | |
|Abonnemententwurf | N/V: wurde für ein einzelnes Produktionsabonnement entworfen. | [Skalieren von Abonnements](../considerations/scaling-subscriptions.md) |
| Verwaltungsgruppen | N/V: wurde für ein einzelnes Produktionsabonnement entworfen. |[Skalieren von Abonnements](../considerations/scaling-subscriptions.md) |
| Ressourcengruppen | N/V: wurde für ein einzelnes Produktionsabonnement entworfen. | [Skalieren von Abonnements](../considerations/scaling-subscriptions.md) |
| Data | – | [Auswählen der richtigen Bereitstellungsoption in Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) und [Auswählen des richtigen Datenspeichers](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Storage|–|[Leitfaden zu Azure Storage](../considerations/storage-guidance.md) |
| Benennungsstandards | Wenn die Umgebung erstellt wird, wird auch ein eindeutiges Präfix erstellt. Für Ressourcen, die einen global eindeutigen Namen benötigen (z. B. Speicherkonten), wird dieses Präfix verwendet. Dem benutzerdefinierten Namen wird ein zufälliges Suffix angefügt. Tags müssen wie in der folgenden Tabelle beschrieben verwendet werden. | [Best Practices zur Benennung und Kennzeichnung](../considerations/naming-and-tagging.md) |
| Kostenverwaltung | – | [Nachverfolgen von Kosten](../azure-best-practices/track-costs.md) |
| Compute | – | [Computeoptionen](../considerations/compute-decisions.md) |

### <a name="tagging-standards"></a>Kennzeichnungsstandards

Bei allen Ressourcen und Ressourcengruppen muss der folgende minimale Satz an Tags vorhanden sein:

| Tag-Name | BESCHREIBUNG | Schlüssel | Beispielwert |
|--|--|--|--|
| Geschäftseinheit | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. | BusinessUnit | FINANCE, MARKETING, {Produktname}, CORP, SHARED |
| Kostenstelle | Buchhaltungskostenstelle, die dieser Ressource zugeordnet ist.| CostCenter | Number |
| Notfallwiederherstellung | Geschäftliche Bedeutung der Anwendung, Workload oder dieses Diensts. | DR | DR-ENABLED, NON-DR-ENABLED |
| Environment | Bereitstellungsumgebung der Anwendung, Workload oder dieses Diensts. |  Env | Prod, Dev, QA, Stage, Test, Training |
| Name des Besitzers | Besitzer der Anwendung, der Workload oder des Diensts.| Owner (Besitzer) | email |
| Bereitstellungstyp | Definiert, wie die Ressourcen verwaltet werden. | deploymentType | Manual, Terraform |
| Version | Version der bereitgestellten Blaupause | version | v0.1 |
| Anwendungsname | Der Name der Anwendung, des Diensts oder der Workload, womit die Ressource verknüpft ist. | ApplicationName | „App-Name“ |

## <a name="customize-and-deploy-your-first-landing-zone"></a>Anpassen und Bereitstellen Ihrer ersten Zielzone

Sie können [Ihre grundlegende Terraform-Zielzone klonen](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready). Sie können einfach mit der Zielzone beginnen, indem Sie die Terraform-Variablen ändern. In unserem Beispiel wird **blueprint_foundations.sandbox.auto.tfvars** verwendet, sodass Terraform automatisch die Werte in dieser Datei für Sie festlegt.

Betrachten wir nun die verschiedenen Variablenabschnitte.

In diesem ersten Objekt erstellen wir zwei Ressourcengruppen in der `southeastasia`-Region mit den Namen „-hub-core-sec“ und „-hub-core-sec“ sowie ein Präfix, das der Runtime hinzugefügt wird.

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

Anschließend geben wir den Protokollanalysenamen und eine Reihe von Lösungen an, die die Bereitstellung analysieren. Hier haben wir Netzwerküberwachung, AD-Bewertung und -Replikation, DNS-Analyse und Key Vault-Analyse beibehalten.

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

## <a name="getting-started"></a>Erste Schritte

Nachdem Sie die Konfiguration überprüft haben, können Sie die Konfiguration wie eine Terraform-Umgebung bereitstellen. Sie sollten jedoch den „rover“ verwenden, einen Docker-Container, der die Bereitstellung von Windows, Linux oder MacOS ermöglicht. Sie können mit dem [„rover“-GitHub-Repository](https://github.com/aztfmod/rover) beginnen.

## <a name="next-steps"></a>Nächste Schritte

Die grundlegende Zielzone bildet die Basis für eine aufgeschlüsselte komplexe Umgebung. Diese Edition bietet eine Reihe sehr einfacher Funktionen, die folgendermaßen erweitert werden kann:

- Hinzufügen weiterer Module zur Blaupause.
- Überlagern mit weiteren Zielzonen.

Das Überlagern mit weiteren Zielzonen ist eine bewährte Vorgehensweise, um Systeme zu entkoppeln, jede einzelne von Ihnen verwendete Komponente zu versionieren und schnelle Innovation und Stabilität für Ihre Infrastructure-as-Code-Bereitstellung zu ermöglichen.

Zukünftige Referenzarchitekturen werden dieses Konzept für eine Hub-and-Spoke-Topologie veranschaulichen.

> [!div class="nextstepaction"]
> [Überprüfen des Beispiels der grundlegenden Zielzone mit Terraform](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready)
