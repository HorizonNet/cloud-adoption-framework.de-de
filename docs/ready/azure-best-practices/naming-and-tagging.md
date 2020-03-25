---
title: Empfohlene Namens- und Kennzeichnungskonventionen
description: Enthält detaillierte Empfehlungen zur Benennung von Ressourcen und zur Kennzeichnung, die speziell auf die Unterstützung der Enterprise Cloud-Einführung ausgerichtet sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/05/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: 9e60e84659828efdc9802c45cf2f91ad945c8cda
ms.sourcegitcommit: 5d7e93540a679252f1c7207e62cb2ee7213a6ae9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80069793"
---
<!-- cSpell:ignore eastus westus westeurope usgovia accountlookup messagequery -->

# <a name="recommended-naming-and-tagging-conventions"></a>Empfohlene Namens- und Kennzeichnungskonventionen

Organisieren Sie Ihre Cloudressourcen so, dass das operative Management und die Buchhaltungsanforderungen unterstützt werden. Gut definierte Namens- und Kennzeichnungskonventionen für Metadaten ermöglichen das schnelle Finden und Verwalten von Ressourcen. Diese Konventionen helfen auch dabei, Cloudnutzungskosten mithilfe von Mechanismen zur Rückbuchung und verbrauchsbasierter Kostenzuteilung an Geschäftsteams auszurichten.

In dem für Azure Architecture Center geltenden Leitfaden zu [Benennungsregeln und -einschränkungen für Azure-Ressourcen](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) finden Sie allgemeine Empfehlungen sowie Informationen zu Plattformeinschränkungen. In den folgenden Erläuterungen wird dieser Leitfaden um detailliertere Empfehlungen erweitert, die speziell zur Unterstützung bei Aktivitäten zur Einführung von Unternehmensclouds vorgesehen sind.

Das Ändern von Ressourcennamen kann schwierig sein. Legen Sie eine umfassende Namenskonvention fest, bevor Sie mit einer größeren Cloudbereitstellung beginnen.

> [!NOTE]
> Jedes Unternehmen hat unterschiedliche Organisations-und Verwaltungsanforderungen. Die Empfehlungen dienen als Ausgangspunkt für Diskussionen in ihren Cloudeinführungsteams.
>
> Verwenden Sie im Verlauf dieser Diskussionen die folgende Vorlage, um die Namens- und Taggingentscheidungen zu erfassen, die Sie treffen, wenn Sie diese Empfehlungen an Ihre speziellen geschäftlichen Anforderungen anpassen.
>
> Laden Sie die [Vorlage zum Festhalten von Namens- und Kennzeichnungskonventionen](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) herunter.

## <a name="naming-and-tagging-resources"></a>Benennen und Kennzeichnen von Ressourcen

Eine Benennungs- und Kennzeichnungsstrategie beinhaltet geschäftliche und operative Details als Komponenten von Ressourcennamen und Metadatentags:

- Mit der unternehmensbezogenen Seite dieser Strategie wird sichergestellt, dass Ressourcennamen und Tags die Organisationsinformationen enthalten, die zum Identifizieren der Teams benötigt werden. Verwenden Sie eine Ressource zusammen mit den Geschäftsbesitzern, die für die Ressourcenkosten verantwortlich sind.
- Die operative Seite stellt sicher, dass Namen und Kennzeichnungen (Tags) Informationen enthalten, anhand denen IT-Teams die Workload, die Anwendung, die Umgebung, die Wichtigkeit und weitere Informationen erkennen können, die für die Verwaltung von Ressourcen nützlich sind.

## <a name="resource-naming"></a>Benennen von Ressourcen

In einer wirkungsvollen Namenskonvention werden Ressourcennamen aus wichtigen Ressourceninformationen als Namensbestandteilen zusammengesetzt. Werden beispielsweise die [empfohlenen Namenskonventionen](#example-names) verwendet, wird eine öffentliche IP-Ressource für eine SharePoint-Produktionsworkload wie folgt benannt: `pip-sharepoint-prod-westus-001`.

Anhand des Namens können Sie schnell den Typ der Ressource, deren zugehörige Workload, deren Bereitstellungsumgebung und die Azure-Region erkennen, in der sie gehostet wird.

### <a name="naming-scope"></a>Namensbereich

Alle Azure-Ressourcentypen weisen einen Bereich auf, der die Ebene definiert, auf der Ressourcennamen eindeutig sein müssen. Eine Ressource muss einen eindeutigen Namen innerhalb ihres Bereichs aufweisen.

Ein virtuelles Netzwerk hat beispielsweise einen Ressourcengruppenbereich, was bedeutet, dass es in einer bestimmten Ressourcengruppe nur ein Netzwerk namens `vnet-prod-westus-001` geben darf. Andere Ressourcengruppen können ihr eigenes virtuelles Netzwerk namens `vnet-prod-westus-001` haben. Subnetze, um ein weiteres Beispiel zu nennen, gehören in den Bereich eines virtuellen Netzwerks. Daher muss jedes Subnetz innerhalb eines virtuellen Netzwerks eindeutig benannt sein.

Einige Ressourcennamen, etwa PaaS-Dienste mit öffentlichen Endpunkten oder DNS-Bezeichnungen virtueller Maschinen, haben globale Bereiche, was bedeutet, dass sie auf der gesamten Azure-Plattform eindeutig sein müssen.

Für Ressourcennamen gelten Längenbeschränkungen. Daher ist es wichtig, den Kontext, der in einen Namen eingebettet ist, mit dessen Bereich und Länge in Einklang zu bringen, wenn Sie Ihre Namenskonventionen entwickeln. Weitere Informationen zu Namensregeln hinsichtlich zulässiger Anzahl von Zeichen, Bereichen und Namenslängen für Ressourcentypen finden Sie unter [Namenskonventionen für Azure-Ressourcen](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming).

### <a name="recommended-naming-components"></a>Empfohlene Namenskomponenten

Wenn Sie Ihre Namenskonvention erstellen, identifizieren Sie die wichtigsten Bestandteile der Informationen, die in einem Ressourcennamen berücksichtigt werden sollen. Unterschiedliche Informationen sind für unterschiedliche Ressourcentypen relevant. Die folgende Liste enthält Beispiele für Informationen, die beim Erstellen von Ressourcennamen nützlich sind.

Verwenden Sie möglichst kurze Namenskomponenten, um zu verhindern, dass die Längenbeschränkungen für Ressourcennamen überschritten werden.

| Namenskomponente            | BESCHREIBUNG                                                                                                                                                                                                      | Beispiele                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Geschäftseinheit               | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann diese Komponente ein einzelnes Organisationselement des Unternehmens auf oberster Ebene darstellen. | _fin_, _mktg_, _produkt_, _it_, _konzern_           |
| Abonnementtyp           | Zusammenfassende Beschreibung des Zwecks des Abonnements, das die Ressource enthält. Häufig nach Umgebungstyp der Bereitstellung oder nach bestimmten Workloads aufgeschlüsselt.                                                       | _Prod_, _Freigabe_, _Client_                       |
| Anwendungs- oder Dienstname | Der Name der Anwendung, der Workload oder des Diensts, zu der oder dem die Ressource gehört.                                                                                                                                    | _navigator_, _emissionen_, _sharepoint_, _hadoop_ |
| Bereitstellungsumgebung      | Die von der Ressource unterstützte Phase des Entwicklungslebenszyklus der Workload.                                                                                                                              | _Prod_, _Entw_, _QA_, _Stage_, _Test_             |
| Region                      | Die Azure-Region, in der die Ressource bereitgestellt wird.                                                                                                                                                                 | _westus_, _eastus2_, _westeurope_, _usgovia_     |

### <a name="recommended-resource-type-prefixes"></a>Empfohlene Präfixe für Ressourcentypen

Jede Workload kann aus vielen einzelne Ressourcen und Diensten bestehen. Ein Einbinden von Ressourcentyppräfixen in Ihre Ressourcennamen erleichtert die visuelle Erkennung von Anwendungs- oder Dienstkomponenten.

Die folgende Liste enthält empfohlene Azure-Ressourcentypenpräfixe, die Sie verwenden sollten, wenn Sie Ihre Namenskonventionen definieren.

<!-- cSpell:disable -->

### <a name="general"></a>Allgemein

| Ressourcentyp                      | Namenspräfix |
|---------------------------------|-------------|
| Resource group                  | rg-         |
| Richtliniendefinition               | policy-     |
| API Management-Dienstinstanz | apim-       |

### <a name="networking"></a>Netzwerk

| Ressourcentyp                       | Namenspräfix |
|----------------------------------|-------------|
| Virtuelles Netzwerk                  | vnet-       |
| Subnet                           | snet-       |
| Netzwerkschnittstelle (NIC)          | nic-        |
| Öffentliche IP-Adresse                | pip-        |
| Lastenausgleich (intern)         | lbi-        |
| Lastenausgleich (extern)         | lbe-        |
| Netzwerksicherheitsgruppe (NSG)     | nsg-        |
| Anwendungssicherheitsgruppe (ASG) | asg-        |
| Lokales Netzwerkgateway            | lgw-        |
| Gateway des virtuellen Netzwerks          | vgw-        |
| VPN-Verbindung                   | cn-         |
| Anwendungsgateway              | agw-        |
| Routingtabelle                      | route-      |
| Traffic Manager-Profil          | traf-       |

### <a name="compute-and-web"></a>Compute und Web

| Ressourcentyp                  | Namenspräfix |
|-----------------------------|-------------|
| Virtueller Computer             | vm          |
| VM-Skalierungsgruppe   | vmss-       |
| Verfügbarkeitsgruppe            | avail-      |
| VM-Speicherkonto          | spvm        |
| Vernetzter Azure Arc-Computer | arcm-       |
| Containerinstanz          | aci-        |
| AKS-Cluster                 | aks-        |
| Service Fabric-Cluster      | sf-         |
| App Service-Umgebung     | ase-        |
| App Service-Plan            | plan-       |
| Web-App                     | app-        |
| Funktionen-App                | func-       |
| Clouddienst               | cld-        |
| Notification Hubs           | ntf-        |
| Notification Hubs-Namespace | ntfns-      |

### <a name="databases"></a>Datenbanken

| Ressourcentyp                     | Namenspräfix |
|--------------------------------|-------------|
| Azure SQL-Datenbank-Server      | sql-        |
| Azure SQL-Datenbank             | sqldb-      |
| Cosmos DB-Datenbank             | cosmos-     |
| Azure Cache for Redis-Instanz | redis-      |
| MySQL-Datenbank                 | mysql-      |
| PostgreSQL-Datenbank            | psql-       |
| Azure SQL Data Warehouse       | sqldw-      |
| Azure Synapse Analytics        | syn-        |
| SQL Server Stretch Database    | sqlstrdb-   |

### <a name="storage"></a>Storage

| Ressourcentyp       | Namenspräfix |
|------------------|-------------|
| Speicherkonto  | st          |
| Azure StorSimple | ssimp       |

### <a name="ai--machine-learning"></a>KI und Machine Learning

| Ressourcentyp                       | Namenspräfix |
|----------------------------------|-------------|
| Azure Cognitive Search           | srch-       |
| Azure Cognitive Services         | cog-        |
| Azure Machine Learning-Arbeitsbereich | mlw-        |

### <a name="analytics-and-iot"></a>Analytics und IoT

| Ressourcentyp                      | Namenspräfix |
|---------------------------------|-------------|
| Azure Analysis Services-Server  | as-         |
| Azure Databricks-Arbeitsbereich      | dbw-        |
| Azure Stream Analytics          | asa-        |
| Azure Data Factory              | adf-        |
| Data Lake Store-Konto         | dls         |
| Data Lake Analytics-Konto     | dla         |
| Event Hub                       | evh-        |
| HDInsight: Hadoop-Cluster      | hadoop-     |
| HDInsight: HBase-Cluster       | hbase-      |
| HDInsight: Kafka-Cluster       | kafka-      |
| HDInsight: Spark-Cluster       | spark-      |
| HDInsight: Storm-Cluster       | storm-      |
| HDInsight: ML Services-Cluster | mls-        |
| IoT Hub                         | iot-        |
| Power BI Embedded               | pbi-        |

### <a name="integration"></a>Integration

| Ressourcentyp        | Namenspräfix |
|-------------------|-------------|
| Logik-Apps        | logic-      |
| Service Bus       | sb-         |
| Service Bus-Warteschlange | sbw-        |
| Service Bus-Topic | sbt-        |

### <a name="management-and-governance"></a>Verwaltung und Governance

| Ressourcentyp              | Namenspräfix |
|-------------------------|-------------|
| Blaupause               | bp-         |
| Schlüsseltresor               | kv-         |
| Log Analytics-Arbeitsbereich | log-        |
| Application Insights    | appi-       |
| Recovery Services-Tresor | rsv-        |

### <a name="migration"></a>Migration

| Ressourcentyp                          | Namenspräfix |
|-------------------------------------|-------------|
| Azure Migrate-Projekt               | migr-       |
| Database Migration Service-Instanz | dms-        |
| Recovery Services-Tresor             | rsv-        |

<!-- cSpell:enable -->

## <a name="metadata-tags"></a>Metadatentags

Wenn Sie Metadatentags auf Ihre Cloudressourcen anwenden, können Sie Informationen zu den Ressourcen einschließen, die nicht im Ressourcennamen enthalten sein konnten. Sie können diese Informationen verwenden, um komplexere Filterung und Berichterstellung für Ressourcen auszuführen. Diese Tags sollten den Kontext zur zugehörigen Workload oder Anwendung der Ressource, betriebliche Anforderungen und Angaben zum Besitzer einbeziehen. Diese Informationen können von IT- oder Geschäftsteams verwendet werden, um Ressourcen zu finden oder Berichte zur Ressourcennutzung und -abrechnung zu generieren.

Welche Tags Sie für Ressourcen anwenden und welche Tags erforderlich oder optional sind, ist von Unternehmen zu Unternehmen unterschiedlich. Die folgende Liste enthält Beispiele für gängige Tags, mit denen wichtige Kontexte und Informationen zu einer Ressource erfasst werden. Verwenden Sie diese Liste als Ausgangspunkt, um eigene Taggingkonventionen einzurichten.

| Tag-Name                  | BESCHREIBUNG                                                                                                                                                                                                          | Schlüssel               | Beispielwert                                              |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|------------------------------------------------------------|
| Anwendungsname          | Der Name der Anwendung, des Diensts oder der Workload, mit der die Ressource verknüpft ist.                                                                                                                                       | _ApplicationName_ | _{App-Name}_                                               |
| Name der genehmigenden Person             | Die Person, die für das Genehmigen der Kosten zuständig ist, die mit dieser Ressource verbunden sind.                                                                                                                                                     | _Approver_        | _{E-Mail}_                                                  |
| Erforderliches/genehmigtes Budget  | Der Geldbetrag, der für diese Anwendung, diesen Dienst oder diese Workload zugeordnet ist.                                                                                                                                                          | _BudgetAmount_    | _{\$}_                                                     |
| Geschäftseinheit             | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann dieses Tag ein einzelnes Organisations- oder freigegebenes Element des Unternehmens auf oberster Ebene darstellen. | _BusinessUnit_    | _FINANZEN_, _MARKETING_, _{Produktname}_ , _CORP_, _FREIGABE_ |
| Kostenstelle               | Buchhaltungskostenstelle, die dieser Ressource zugeordnet ist.                                                                                                                                                                | _CostCenter_      | _{Zahl}_                                                 |
| Notfallwiederherstellung         | Geschäftliche Bedeutung der Anwendung, Workload oder dieses Diensts.                                                                                                                                                       | _DR_              | _Unternehmenskritisch_, _Kritisch_, _Unverzichtbar_                |
| Enddatum des Projekts   | Datum, zu dem die Deaktivierung der Anwendung, Workload oder dieses Diensts geplant ist.                                                                                                                                         | _EndDate_         | _{Datum}_                                                   |
| Environment               | Bereitstellungsumgebung der Anwendung, Workload oder dieses Diensts.                                                                                                                                                     | _Env_             | _Prod_, _Entw_, _QA_, _Stage_, _Test_                       |
| Name des Besitzers                | Besitzer der Anwendung, der Workload oder des Diensts.                                                                                                                                                                      | _Besitzer_           | _{E-Mail}_                                                  |
| Name der anfordernden Person            | Der Benutzer, der die Erstellung dieser Anwendung angefordert hat.                                                                                                                                                                 | _Requestor_       | _{E-Mail}_                                                  |
| Dienstklasse             | Vereinbarung zum Servicelevel der Anwendung, der Workload oder des Diensts.                                                                                                                                              | _ServiceClass_    | _Dev_, _Bronze_, _Silver_, _Gold_                          |
| Startdatum des Projekts | Datum, zu dem die Anwendung, Workload oder dieser Dienst erstmalig bereitgestellt wurde.                                                                                                                                                  | _StartDate_       | _{Datum}_                                                   |

## <a name="example-names"></a>Namensbeispiele

Der folgende Abschnitt enthält einige Namensbeispiele für häufige Azure-Ressourcentypen bei der Bereitstellung einer Unternehmenscloud.

<!-- cSpell:disable -->

<!-- markdownlint-disable MD024 MD033 -->

### <a name="example-names-general"></a>Namensbeispiele: Allgemein

| Ressourcentyp                      | `Scope`                              | Format                                                      | Beispiele                                                                                                                |
|---------------------------------|------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Subscription                    | Account/ <br/>Enterprise Agreement | \<Geschäftseinheit\>-\<Abonnementtyp\>-\<\#\#\#\>          | <ul><li>mktg-prod-001 </li><li>konzern-freigabe-001 </li><li>fin-client-001</li></ul>                                        |
| Resource group                  | Subscription                       | rg-\<App- oder Dienstname\>-\<Abonnementtyp\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-kontnachschldien-freigabe-001 </li><li>rg-ad-verz-dienste-freigabe-001</li></ul> |
| API Management-Dienstinstanz | Global                             | apim-\<App- oder Dienstname\>                                | apim-navigator-prod                                                                                                     |

### <a name="example-names-networking"></a>Namensbeispiele: Netzwerk

| Ressourcentyp                   | `Scope`           | Format                                                               | Beispiele                                                                                                                      |
|------------------------------|-----------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Virtuelles Netzwerk              | Resource group  | vnet-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                     | <ul><li>vnet-freigabe-usaosten2-001 </li><li>vnet-prod-usawesten-001 </li><li>vnet-client-usaosten2-001</li></ul>                      |
| Subnet                       | Virtuelles Netzwerk | snet-\<Abonnement\>-\<Unterregion\>-\<\#\#\#\>                       | <ul><li>snet-freigabe-usaosten2-001 </li><li>snet-prod-usawesten-001 </li><li>snet-client-usaosten2-001</li></ul>                      |
| Netzwerkschnittstelle (NIC)      | Resource group  | nic-\<\#\#\>-\<VM-Name\>-\<Abonnement\>\<\#\#\#\>                   | <ul><li>nic-01-dc1-freigabe-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>                 |
| Öffentliche IP-Adresse            | Resource group  | pip-\<VM-Name oder App-Namen\>-\<Umgebung\>-\<Unterregion\>-\<\#\#\#\> | <ul><li>pip-dc1-freigabe-usaosten2-001 </li><li>pip-hadoop-prod-usawesten-001</li></ul>                                              |
| Load Balancer                | Resource group  | lb-\<App-Name oder Rolle\>\<Umgebung\>\<\#\#\#\>                     | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-entw-001</li></ul>                                                        |
| Netzwerksicherheitsgruppe (NSG) | Subnetz oder NIC   | nsg-\<Richtlinienname oder App-Name\>-\<\#\#\#\>                           | <ul><li>nsg-weberlaub-001 </li><li>nsg-rdperlaub-001 </li><li>nsg-sqlerlaub-001 </li><li>nsg-dnsblockier-001</li></ul>             |
| Lokales Netzwerkgateway        | Virtuelles Gateway | lgw-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                      | <ul><li>lgw-shared-eastus2-001 </li><li>lgw-prod-westus-001 </li><li>lgw-client-eastus2-001</li></ul>                         |
| Gateway des virtuellen Netzwerks      | Virtuelles Netzwerk | vgw-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vgw-shared-eastus2-001 </li><li>vgw-prod-westus-001 </li><li>vgw-client-eastus2-001</li></ul>                         |
| Standort-zu-Standort-Verbindung      | Resource group  | cn-\<Name des lokalen Gateways\>-to-\<Name des virtuellen Gateways\>                | <ul><li>cn-lgw-shared-eastus2-001-to-vgw-shared-eastus2-001 </li><li>cn-lgw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| VPN-Verbindung               | Resource group  | cn-\<Abonnement1\>\<Region1\>-to-\<Abonnement2\>\<Region2\>-     | <ul><li>cn-freigabe-usaosten2-to-freigabe-usawesten </li><li>cn-prod-usaosten2-to-prod-usawesten</li></ul>                                  |
| Routingtabelle                  | Resource group  | route-\<Name der Routentabelle\>                                           | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-entw-001</li></ul>                                                        |
| DNS-Bezeichnung                    | Global          | \<Eintrag von VM\>.[\<Region\>.cloudapp.azure.com]                   | <ul><li>dc1.usawesten.cloudapp.azure.com </li><li>web1.usaosten2.cloudapp.azure.com</li></ul>                                      |

### <a name="example-names-compute-and-web"></a>Namensbeispiele: Compute und Web

| Ressourcentyp                  | `Scope`          | Format                                                              | Beispiele                                                                                                                          |
|-----------------------------|----------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Virtueller Computer             | Resource group | vm-\<Richtlinienname oder App-Name\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlknoten001 </li><li>vmhadoop001</li></ul>                              |
| VM-Speicherkonto          | Global         | stvm\<Leistungstyp\>\<App-Name oder Produktname\>\<Region\>\<\#\#\#\> | <ul><li>stvmstcoreusaosten2001 </li><li>stvmpmcoreusaosten2001 </li><li>stvmstplmusaosten2001 </li><li>stvmsthadoopusaosten2001</li></ul> |
| Web-App                     | Global         | app-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{azurewebsites.net}]   | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Funktionen-App                | Global         | func-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{azurewebsites.net}]  | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul>                 |
| Clouddienst               | Global         | cld-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{cloudapp.net}]        | <ul><li>cld-navigator-prod-001.azurewebsites.net </li><li>cld-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Notification Hub            | Resource group | ntf-\<App-Name\>-\<Umgebung\>                                    | <ul><li>ntf-navigator-prod </li><li>ntf-emissions-dev</li></ul>                                                                   |
| Notification Hubs-Namespace | Global         | ntfns-\<App-Name\>-\<Umgebung\>                                  | <ul><li>ntfns-navigator-prod </li><li>ntfns-emissions-dev</li></ul>                                                               |

### <a name="example-names-databases"></a>Namensbeispiele: Datenbanken

| Ressourcentyp                     | `Scope`              | Format                                 | Beispiele                                                                  |
|--------------------------------|--------------------|----------------------------------------|---------------------------------------------------------------------------|
| Azure SQL-Datenbank-Server      | Global             | sql-\<App-Name\>-\<Umgebung\>       | <ul><li>sql-navigator-prod </li><li>sql-emissions-dev</li></ul>           |
| Azure SQL-Datenbank             | Azure SQL-Datenbank | sqldb-\<Datenbankname>-\<Umgebung\> | <ul><li>sqldb-users-prod </li><li>sqldb-users-dev</li></ul>               |
| Cosmos DB-Datenbank             | Global             | cosmos-\<App-Name\>-\<Umgebung\>    | <ul><li>cosmos-navigator-prod </li><li>cosmos-emissions-dev</li></ul>     |
| Azure Cache for Redis-Instanz | Global             | redis-\<App-Name\>-\<Umgebung\>     | <ul><li>redis-navigator-prod </li><li>redis-emissionen-entw</li></ul>       |
| MySQL-Datenbank                 | Global             | mysql-\<App-Name\>-\<Umgebung\>     | <ul><li>mysql-navigator-prod </li><li>mysql-emissionen-entw</li></ul>       |
| PostgreSQL-Datenbank            | Global             | psql-\<App-Name\>-\<Umgebung\>      | <ul><li>psql-navigator-prod </li><li>psql-emissions-dev</li></ul>         |
| Azure SQL Data Warehouse       | Global             | sqldw-\<App-Name\>-\<Umgebung\>     | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissionen-entw</li></ul>       |
| SQL Server Stretch Database    | Azure SQL-Datenbank | sqlstrdb-\<App-Name\>-\<Umgebung\>  | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissionen-entw</li></ul> |

### <a name="example-names-storage"></a>Namensbeispiele: Storage

| Ressourcentyp                        | `Scope`  | Format                                                                        | Beispiele                                                              |
|-----------------------------------|--------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Speicherkonto (allgemeine Nutzung)     | Global | st\<Speichername\>\<\#\#\#\>                                                  | <ul><li>stnavigatordaten001 </li><li>stemissionenausgabe001</li></ul>    |
| Speicherkonto (Diagnoseprotokolle) | Global | stdiag\<erste 2 Buchstaben vom Abonnementnamen und die Nummer\>\<Region\>\<\#\#\#\> | <ul><li>stdiagsh001usaosten2001 </li><li>stdiagsh001usawesten001</li></ul> |
| Azure StorSimple                  | Global | ssimp\<App-Name\>\<Umgebung\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionenentw</li></ul>       |

### <a name="example-names-ai--machine-learning"></a>Namensbeispiele: KI und Machine Learning

| Ressourcentyp                       | `Scope`          | Format                            | Beispiele                                                          |
|----------------------------------|----------------|-----------------------------------|-------------------------------------------------------------------|
| Azure Cognitive Search           | Global         | srch-\<App-Name\>-\<Umgebung\> | <ul><li>srch-navigator-prod </li><li>srch-emissionen-entw</li></ul> |
| Azure Cognitive Services         | Resource group | cog-\<App-Name\>-\<Umgebung\>  | <ul><li>cog-navigator-prod </li><li>cog-emissions-dev</li></ul>   |
| Azure Machine Learning-Arbeitsbereich | Resource group | mlw-\<App-Name\>-\<Umgebung\>  | <ul><li>mlw-navigator-prod </li><li>mlw-emissions-dev</li></ul>   |

### <a name="example-names-analytics-and-iot"></a>Namensbeispiele: Analytics und IoT

| Ressourcentyp                  | `Scope`          | Format                              | Beispiele                                                              |
|-----------------------------|----------------|-------------------------------------|-----------------------------------------------------------------------|
| Azure Data Factory          | Global         | adf-\<App-Name\>\<Umgebung\>     | <ul><li>adf-navigator-prod </li><li>adf-emissions-dev</li></ul>       |
| Azure Stream Analytics      | Resource group | asa-\<App-Name\>-\<Umgebung\>    | <ul><li>asa-navigator-prod </li><li>asa-emissionen-entw</li></ul>       |
| Data Lake Analytics-Konto | Global         | dla\<App-Name\>\<Umgebung\>      | <ul><li>dlanavigatorprod </li><li>dlaemissionenentw</li></ul>           |
| Data Lake Storage-Konto   | Global         | dls\<App-Name\>\<Umgebung\>      | <ul><li>dlsnavigatorprod </li><li>dlsemissionenentw</li></ul>           |
| Event Hub                   | Global         | evh-\<App-Name\>-\<Umgebung\>    | <ul><li>anh-navigator-prod </li><li>anh-emissionen-entw</li></ul>       |
| HDInsight: HBase-Cluster   | Global         | hbase-\<App-Name\>-\<Umgebung\>  | <ul><li>hbase-navigator-prod </li><li>hbase-emissions-dev</li></ul>   |
| HDInsight: Hadoop-Cluster  | Global         | hadoop-\<App-Name\>-\<Umgebung\> | <ul><li>hadoop-navigator-prod </li><li>hadoop-emissions-dev</li></ul> |
| HDInsight: Spark-Cluster   | Global         | spark-\<App-Name\>-\<Umgebung\>  | <ul><li>spark-navigator-prod </li><li>spark-emissions-dev </li></ul>  |
| IoT Hub                     | Global         | iot-\<App-Name\>-\<Umgebung\>    | <ul><li>iot-navigator-prod </li><li>iot-emissions-dev</li></ul>       |
| Power BI Embedded           | Global         | pbi-\<App-Name\>\<Umgebung\>     | <ul><li>pbi-navigator-prod </li><li>pbi-emissions-dev</li></ul>       |

### <a name="example-names-integration"></a>Namensbeispiele: Integration

| Ressourcentyp        | `Scope`       | Format                                                     | Beispiele                                                      |
|-------------------|-------------|------------------------------------------------------------|---------------------------------------------------------------|
| Service Bus       | Global      | sb-\<App-Name\>-\<Umgebung\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissionen-entw</li></ul> |
| Service Bus-Warteschlange | Service Bus | sbq-\<Abfragedeskriptor\>                                   | <ul><li>sbq-nachrabfrage</li></ul>                            |
| Service Bus-Topic | Service Bus | sbt-\<Abfragedeskriptor\>                                   | <ul><li>sbt-messagequery</li></ul>                            |
