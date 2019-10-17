---
title: 'Bereit: Empfohlene Namens- und Kennzeichnungskonventionen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dieser Artikel enthält detaillierte Empfehlungen zur Benennung von Ressourcen und zur Kennzeichnung, die speziell auf die Unterstützung der Enterprise Cloud-Einführung ausgerichtet sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: 003e212326959b593071f8230d2ddc0dba646909
ms.sourcegitcommit: b30952f08155513480c6b2c47a40271c2b2357cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72378282"
---
# <a name="ready-recommended-naming-and-tagging-conventions"></a>Bereit: Empfohlene Namens- und Kennzeichnungskonventionen

Das Verwalten von cloudbasierten Ressourcen in einer Weise, die das operative Management und die Buchhaltungsanforderungen unterstützt, ist eine häufige Herausforderung, die große Anstrengungen bei der Einführung von Cloudaktivitäten bedingt. Indem Sie klar definierte Benennungs- und Metadatentaggingkonventionen auf in der Cloud gehostete Ressourcen anwenden, können IT-Mitarbeiter Ressourcen schnell finden und verwalten. Klar definierte Namen und Tags helfen auch, Cloudressourcenkosten mithilfe von Mechanismen zur Rückbuchung und verbrauchsbasierter Kostenzuteilung an Geschäftsteams auszurichten.

In dem für Azure Architecture Center geltenden Leitfaden [Benennungsregeln und -einschränkungen für Azure-Ressourcen](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) finden Sie allgemeine Empfehlungen für Namenskonventionen sowie Erläuterungen zu Namenseinschränkungen und Plattformregeln. In den folgenden Erläuterungen wird dieser allgemeine Leitfaden um detailliertere Empfehlungen erweitert, die speziell zur Unterstützung bei Aktivitäten zur Einführung von Unternehmensclouds vorgesehen sind.

Das Ändern von Ressourcennamen kann schwierig sein. Daher sollten Sie das Einführen einer umfassenden Namenskonvention zu einer Priorität für Ihre Cloudeinführungsteams erklären, bevor Sie mit jeder größeren Cloudbereitstellung beginnen.

> [!NOTE]
> Jedes Unternehmen hat unterschiedliche Organisations-und Verwaltungsanforderungen. Die Empfehlungen in diesem Artikel dienen als Ausgangspunkt für Diskussionen in ihren Cloudeinführungsteams.
>
> Verwenden Sie im Verlauf dieser Diskussionen die folgende Vorlage, um die Namens- und Taggingentscheidungen zu erfassen, die Sie treffen, wenn Sie diese Empfehlungen an Ihre speziellen geschäftlichen Anforderungen anpassen.
>
> Laden Sie die [Vorlage zum Festhalten von Namens- und Kennzeichnungskonventionen](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) herunter.

## <a name="naming-and-tagging-resources"></a>Benennen und Kennzeichnen von Ressourcen

Eine Benennungs- und Kennzeichnungsstrategie beinhaltet geschäftliche und operative Details als Komponenten von Ressourcennamen und Metadatentags:

- Die unternehmensbezogene Seite dieser Strategie stellt sicher, dass Ressourcennamen und Tags die Organisationsinformationen enthalten, die zum Identifizieren der Teams benötigt werden. Verwenden Sie eine Ressource zusammen mit den Geschäftsbesitzern, die für die Ressourcenkosten verantwortlich sind.
- Die operative Seite stellt sicher, dass Namen und Kennzeichnungen (Tags) Informationen enthalten, anhand denen IT-Teams die Workload, die Anwendung, die Umgebung, die Wichtigkeit und weitere Informationen erkennen können, die für die Verwaltung von Ressourcen nützlich sind.

### <a name="resource-naming"></a>Benennen von Ressourcen

In einer wirkungsvollen Namenskonvention werden Ressourcennamen aus wichtigen Ressourceninformationen als Namensbestandteilen zusammengesetzt. Werden beispielsweise die empfohlenen Namenskonventionen verwendet, die [weiter unten in diesem Artikel](#sample-naming-convention) erläutert sind, wird eine öffentliche IP-Ressource für eine SharePoint-Produktionsworkload wie folgt benannt: `pip-sharepoint-prod-westus-001`.

Anhand des Namens können Sie schnell den Typ der Ressource, deren zugehörige Workload, deren Bereitstellungsumgebung und die Azure-Region erkennen, in der sie gehostet wird.

#### <a name="naming-scope"></a>Namensbereich

Für alle Azure-Ressourcentypen gibt es einen Bereich, über den definiert wird, wie diese Ressourcen relativ zu anderen Ressourcentypen verwaltet werden können. Hinsichtlich der Namenskonventionen bedeutet dies, dass eine Ressource einen eindeutigen Namen innerhalb ihres Bereichs haben muss.

Ein virtuelles Netzwerk hat beispielsweise einen Ressourcengruppenbereich, was bedeutet, dass es in einer bestimmten Ressourcengruppe nur ein Netzwerk namens `vnet-prod-westus-001` geben darf. Andere Ressourcengruppen können ihr eigenes virtuelles Netzwerk namens `vnet-prod-westus-001` haben. Subnetze, um ein weiteres Beispiel zu nennen, gehören in den Bereich eines virtuellen Netzwerks. Daher muss jedes Subnetz innerhalb eines virtuellen Netzwerks eindeutig benannt sein.

Einige Ressourcennamen, etwa PaaS-Dienste mit öffentlichen Endpunkten oder DNS-Bezeichnungen virtueller Maschinen, haben globale Bereiche, was bedeutet, dass sie auf der gesamten Azure-Plattform eindeutig sein müssen.

Für Ressourcennamen gelten Längenbeschränkungen. Daher ist es wichtig, den Kontext, der in einen Namen eingebettet ist, mit dessen Bereich und Länge in Einklang zu bringen, wenn Sie Ihre Namenskonventionen entwickeln. Weitere Informationen zu Namensregeln hinsichtlich zulässiger Anzahl von Zeichen, Bereichen und Namenslängen für Ressourcentypen finden Sie unter [Namenskonventionen für Azure-Ressourcen](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).

#### <a name="recommended-naming-components"></a>Empfohlene Namenskomponenten

Wenn Sie Ihre Namenskonvention erstellen, identifizieren Sie die wichtigsten Bestandteile der Informationen, die in einem Ressourcennamen berücksichtigt werden sollen. Unterschiedliche Informationen sind für unterschiedliche Ressourcentypen relevant. Die folgende Liste enthält Beispiele für Informationen, die beim Erstellen von Ressourcennamen nützlich sind.

Verwenden Sie möglichst kurze Namenskomponenten, um zu verhindern, dass die Längenbeschränkungen für Ressourcennamen überschritten werden.

| Namenskomponente | BESCHREIBUNG | Beispiele |
| --- | --- | --- |
| Geschäftseinheit | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann diese Komponente ein einzelnes Organisationselement des Unternehmens auf oberster Ebene darstellen. | *fin*, *mktg*, *produkt*, *it*, *konzern* |
| Abonnementtyp | Zusammenfassende Beschreibung des Zwecks des Abonnements, das die Ressource enthält. Häufig nach Umgebungstyp der Bereitstellung oder nach bestimmten Workloads aufgeschlüsselt. | *prod,* *freigabe, client* |
| Anwendungs- oder Dienstname | Der Name der Anwendung, der Workload oder des Diensts, zu der oder dem die Ressource gehört. | *navigator*, *emissionen*, *sharepoint*, *hadoop* |
| Bereitstellungsumgebung | Die von der Ressource unterstützte Phase des Entwicklungslebenszyklus der Workload. | *prod, entw, qs, phase, test* |
| Region | Die Azure-Region, in der die Ressource bereitgestellt wird. | *usawesten, usaosten2, europawesten, usgovia* |

#### <a name="recommended-resource-type-prefixes"></a>Empfohlene Präfixe für Ressourcentypen

Jede Workload kann aus vielen einzelne Ressourcen und Diensten bestehen. Ein Einbinden von Ressourcentyppräfixen in Ihre Ressourcennamen erleichtert die visuelle Erkennung von Anwendungs- oder Dienstkomponenten.

Die folgende Liste enthält empfohlene Azure-Ressourcentypenpräfixe, die Sie verwenden sollten, wenn Sie Ihre Namenskonventionen definieren.

| Ressourcentyp                       | Präfix für Ressourcenname |
| ----------------------------------- | -------------------- |
| Resource group                      | rg-                  |
| Virtuelles Azure-Netzwerk                     | vnet-                |
| Gateway des virtuellen Netzwerks             | vnet-gw-             |
| Gatewayverbindung                  | cn-                  |
| Subnet                              | snet-                |
| Netzwerksicherheitsgruppe              | nsg-                 |
| Azure Virtual Machines                    | vm-                  |
| VM-Speicherkonto                  | spvm                 |
| Öffentliche IP-Adresse                           | pip-                 |
| Azure Load Balancer                       | lb-                  |
| NIC                                 | nic-                 |
| Azure-Servicebus                         | sb-                  |
| Azure Service Bus-Warteschlangen                  | sbw-                 |
| Azure App Service-Apps                    | azapp-               |
| Azure Functions-Apps                       | azfun-               |
| Azure Cloud Services                      | azcs-                |
| Azure SQL-Datenbank                  | sqldb-               |
| Azure Cosmos DB (ehemals Azure DocumentDB) | cosdb-               |
| Azure Cache for Redis               | redis-               |
| Azure Database for MySQL            | mysql-               |
| Azure SQL Data Warehouse                  | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Azure Storage                       | stor                 |
| Azure StorSimple                          | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services                  | cs-                  |
| Azure Machine Learning-Arbeitsbereich    | aml-                 |
| Azure Data Lake Store             | dls                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight: Spark                   | hdis-                |
| Azure HDInsight: Hadoop                  | hdihd-               |
| Azure HDInsight: R Server                | hdir-                |
| Azure HDInsight: HBase                   | hdihb-               |
| Power BI Embedded                   | pbiemb               |
| Azure Stream Analytics                    | asa-                 |
| Azure Data Factory                        | df-                  |
| Azure Event Hubs                           | evh-                 |
| Azure IoT Hub                       | aih-                 |
| Azure Notification Hubs                   | anh-                 |
| Azure Notification Hubs-Namespace          | anhns-               |

### <a name="metadata-tags"></a>Metadatentags

Wenn Sie Metadatentags auf Ihre Cloudressourcen anwenden, können Sie Informationen zu den Ressourcen einschließen, die nicht im Ressourcennamen enthalten sein konnten. Sie können diese Informationen verwenden, um komplexere Filterung und Berichterstellung für Ressourcen auszuführen. Diese Tags sollten den Kontext zur zugehörigen Workload oder Anwendung der Ressource, betriebliche Anforderungen und Angaben zum Besitzer einbeziehen. Diese Informationen können von IT- oder Geschäftsteams verwendet werden, um Ressourcen zu finden oder Berichte zur Ressourcennutzung und -abrechnung zu generieren.

Welche Tags Sie für Ressourcen anwenden und welche Tags erforderlich oder optional sind, ist von Unternehmen zu Unternehmen unterschiedlich. Die folgende Liste enthält Beispiele für gängige Tags, mit denen wichtige Kontexte und Informationen zu einer Ressource erfasst werden. Verwenden Sie diese Liste als Ausgangspunkt, um eigene Taggingkonventionen einzurichten.

| Tag-Name                  | BESCHREIBUNG                                                                                                                                                                                                    | Schlüssel               | Beispielwert                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Anwendungsname          | Der Name der Anwendung, des Diensts oder der Workload, mit der die Ressource verknüpft ist.                                                                                                                                 | *ApplicationName* | *{App-Name}*                                    |
| Name der genehmigenden Person             | Die Person, die für das Genehmigen der Kosten zuständig ist, die mit dieser Ressource verbunden sind.                                                                                                                                               | *Approver*        | *{E-Mail}*                                       |
| Erforderliches/genehmigtes Budget  | Der Geldbetrag, der für diese Anwendung, diesen Dienst oder diese Workload zugeordnet ist.                                                                                                                                                    | *BudgetAmount*    | *{\$}*                                          |
| Geschäftseinheit             | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann dieses Tag ein einzelnes Organisations- oder freigegebenes Element des Unternehmens auf oberster Ebene darstellen. | *BusinessUnit*    | *FINANZEN, MARKETING, {Produktname}, CORP, FREIGABE* |
| Kostenstelle               | Buchhaltungskostenstelle, die dieser Ressource zugeordnet ist.                                                                                                                                                          | *CostCenter*      | *{Zahl}*                                      |
| Notfallwiederherstellung         | Geschäftliche Bedeutung der Anwendung, Workload oder dieses Diensts.                                                                                                                                                | *DR*              | *Unternehmenskritisch, Kritisch, Unverzichtbar*         |
| Enddatum des Projekts   | Datum, zu dem die Deaktivierung der Anwendung, Workload oder dieses Diensts geplant ist.                                                                                                                                  | *EndDate*         | *{Datum}*                                        |
| Environment               | Bereitstellungsumgebung der Anwendung, Workload oder dieses Diensts.                                                                                                                                              | *Env*             | *Prod, Entw, QS, Phase, Test*                    |
| Name des Besitzers                | Besitzer der Anwendung, der Workload oder des Diensts.                                                                                                                                                                | *Besitzer*           | *{E-Mail}*                                       |
| Name der anfordernden Person            | Der Benutzer, der die Erstellung dieser Anwendung angefordert hat.                                                                                                                                                          | *Requestor*       | *{E-Mail}*                                       |
| Dienstklasse             | Vereinbarung zum Servicelevel der Anwendung, der Workload oder des Diensts.                                                                                                                                       | *ServiceClass*    | *Dev, Bronze, Silver, Gold*                     |
| Startdatum des Projekts | Datum, zu dem die Anwendung, Workload oder dieser Dienst erstmalig bereitgestellt wurde.                                                                                                                                           | *StartDate*       | *{Datum}*                                        |

## <a name="sample-naming-convention"></a>Beispielnamenskonvention

Der folgende Abschnitt enthält Beispiele zu Namensschemas für gängige Azure-Ressourcentypen, die während der Bereitstellung einer Unternehmenscloud bereitgestellt werden.

<!-- markdownlint-disable MD033 -->

### <a name="subscriptions"></a>Abonnements

| Ressourcentyp   | `Scope`                        | Format                                             | Beispiele                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Subscription | Konto/Enterprise Agreement | \<Geschäftseinheit\>-\<Abonnementtyp\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>konzern-freigabe-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Ressourcengruppen

| Ressourcentyp     | `Scope`        | Format                                                     | Beispiele                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Resource group | Subscription | rg-\<App-/Dienstname\>-\<Abonnementtyp\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-kontnachschldien-freigabe-001 </li><li>rg-ad-verz-dienste-freigabe-001</li></ul> |

### <a name="virtual-networking"></a>Virtuelle Netzwerke

| Ressourcentyp               | `Scope`           | Format                                                                | Beispiele                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Virtuelles Azure-Netzwerk          | Resource group  | vnet-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vnet-freigabe-usaosten2-001 </li><li>vnet-prod-usawesten-001 </li><li>vnet-client-usaosten2-001</li></ul>                                  |
| Virtuelles Gateway des virtuellen Netzwerks     | Virtuelles Netzwerk | vnet-gw-v-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-v-freigabe-usaosten2-001 </li><li>vnet-gw-v-prod-usawesten-001 </li><li>vnet-gw-v-client-usaosten2-001</li></ul>                   |
| Lokales Gateway des virtuellen Netzwerks       | Virtuelles Gateway | vnet-gw-l-\<Abonnementtyp\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-l-shared-freigabe-usaosten2-001 </li><li>vnet-gw-l-prod-usawesten-001 </li><li>vnet-gw-l-client-usaosten2-001</li></ul>                   |
| Site-to-Site-Verbindungen | Resource group  | cn-\<Name des lokalen Gateways\>-to-\<Name des virtuellen Gateways\>                 | <ul><li>cn-l-gw-freigabe-usaosten2-001-to-v-gw-freigabe-usaosten2-001 </li><li>cn-l-gw-freigabe-usaosten2-001-to-freigabe-usawesten-001</li></ul> |
| Virtuelle Netzwerkverbindungen         | Resource group  | cn-\<Abonnement1\>\<Region1\>-to-\<Abonnement2\>\<Region2\>-      | <ul><li>cn-freigabe-usaosten2-to-freigabe-usawesten </li><li>cn-prod-usaosten2-to-prod-usawesten</li></ul>                                     |
| Subnet                   | Virtuelles Netzwerk | snet-\<Abonnement\>-\<Unterregion\>-\<\#\#\#\>                       | <ul><li>snet-freigabe-usaosten2-001 </li><li>snet-prod-usawesten-001 </li><li>snet-client-usaosten2-001</li></ul>                                  |
| Netzwerksicherheitsgruppe   | Subnetz oder NIC   | nsg-\<Richtlinienname oder App-Name\>-\<\#\#\#\>                             | <ul><li>nsg-weberlaub-001 </li><li>nsg-rdperlaub-001 </li><li>nsg-sqlerlaub-001 </li><li>nsg-dnsblockier-001</li></ul>                                  |
| Öffentliche IP-Adresse                | Resource group  | pip-\<VM-Name oder App-Namen\>-\<Umgebung\>-\<Unterregion\>-\<\#\#\#\> | <ul><li>pip-dc1-freigabe-usaosten2-001 </li><li>pip-hadoop-prod-usawesten-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Ressourcentyp         | `Scope`          | Format                                                              | Beispiele                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Resource group | vm-\<Richtlinienname oder App-Name\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlknoten001 </li><li>vmhadoop001</li></ul>                              |
| VM-Speicherkonto | Global         | stvm\<Leistungstyp\>\<App-Name oder Produktname\>\<Region\>\<\#\#\#\> | <ul><li>stvmstcoreusaosten2001 </li><li>stvmpmcoreusaosten2001 </li><li>stvmstplmusaosten2001 </li><li>stvmsthadoopusaosten2001</li></ul> |
| DNS-Bezeichnung          | Global         | \<Eintrag von VM\>.[\<Region\>.cloudapp.azure.com]                  | <ul><li>dc1.usawesten.cloudapp.azure.com </li><li>web1.usaosten2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Resource group | lb-\<App-Name oder Rolle\>\<Umgebung\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-entw-001</li></ul>                                          |
| NIC                | Resource group | nic-\<\#\#\>-\<VM-Name\>-\<Abonnement\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-freigabe-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>PaaS-Dienste

| Ressourcentyp     | `Scope`  | Format                                                              | Beispiele                                                                                 |
|----------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure App Service    | Global | azapp-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azapp-navigator-prod-001.azurewebsites.net </li><li>azapp-kontonachschl-entw-001.azurewebsites.net</li></ul> |
| Azure Functions-App   | Global | azfun-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azfun-navigator-prod-001.azurewebsites.net </li><li>azfun-kontonachschl-entw-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Global | azcs-\<App-Name\>-\<Umgebung\>-\<\#\#\#\>.[{cloudapp.net}]       | <ul><li>azcs-navigator-prod-001.azurewebsites.net </li><li>azcs-kontonachschl-entw-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure-Servicebus

| Ressourcentyp         | `Scope`       | Format                                                     | Beispiele                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure-Servicebus        | Global      | sb-\<App-Name\>-\<Umgebung\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissionen-entw</li></ul> |
| Azure Service Bus-Warteschlangen | Service Bus | sbq-\<Abfragedeskriptor\>                                   | <ul><li>sbq-nachrabfrage</li></ul>                   |

### <a name="databases"></a>Datenbanken

| Ressourcentyp                          | `Scope`              | Format                                | Beispiele                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL-Datenbank                  | Global             | sqldb-\<App-Name\>-\<Umgebung\>    | <ul><li>sqldb-navigator-prod </li><li>sqldb-emissionen-entw</li></ul>       |
| Azure Cosmos DB (ehemals DocumentDB) | Global             | cosdb-\<App-Name\>-\<Umgebung\>    | <ul><li>cosdb-navigator-prod </li><li>cosdb-emissionen-entw</li></ul>       |
| Azure Cache for Redis               | Global             | redis-\<App-Name\>-\<Umgebung\>    | <ul><li>redis-navigator-prod </li><li>redis-emissionen-entw</li></ul>       |
| Azure Database for MySQL            | Global             | mysql-\<App-Name\>-\<Umgebung\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissionen-entw</li></ul>       |
| Azure SQL Data Warehouse                  | Global             | sqldw-\<App-Name\>-\<Umgebung\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissionen-entw</li></ul>       |
| SQL Server Stretch Database         | Azure SQL-Datenbank | sqlstrdb-\<App-Name\>-\<Umgebung\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissionen-entw</li></ul> |

### <a name="storage"></a>Storage

| Ressourcentyp                              | `Scope`  | Format                                                                        | Beispiele                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Azure Storage-Konto – allgemeine Nutzung     | Global | st\<Speichername\>\<\#\#\#\>                                                  | <ul><li>stnavigatordaten001 </li><li>stemissionenausgabe001</li></ul>    |
| Azure Storage-Konto – Diagnoseprotokolle | Global | stdiag\<erste 2 Buchstaben vom Abonnementnamen und die Nummer\>\<Region\>\<\#\#\#\> | <ul><li>stdiagsh001usaosten2001 </li><li>stdiagsh001usawesten001</li></ul> |
| Azure StorSimple                              | Global | ssimp\<App-Name\>\<Umgebung\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionenentw</li></ul>       |

### <a name="ai--machine-learning"></a>KI und Machine Learning

| Ressourcentyp                       | `Scope`          | Format                            | Beispiele                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Global         | srch-\<App-Name\>-\<Umgebung\> | <ul><li>srch-navigator-prod </li><li>srch-emissionen-entw</li></ul> |
| Azure Cognitive Services               | Resource group | cs-\<App-Name\>-\<Umgebung\>   | <ul><li>cs-navigator-prod </li><li>cs-emissionen-entw</li></ul>     |
| Azure Machine Learning-Arbeitsbereich | Resource group | aml-\<App-Name\>-\<Umgebung\>  | <ul><li>aml-navigator-prod </li><li>aml-emissionen-entw</li></ul>   |

### <a name="analytics"></a>Analytics

| Ressourcentyp                | `Scope`  | Format                             | Beispiele                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Global | df-\<App-Name\>\<Umgebung\>     | <ul><li>df-navigator-prod </li><li>df-emissionen-entw</li></ul>       |
| Azure Data Lake Store   | Global | dls\<App-Name\>\<Umgebung\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionenentw</li></ul>         |
| Azure Data Lake Analytics | Global | dla\<App-Name\>\<Umgebung\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionenentw</li></ul>         |
| Azure HDInsight: Spark         | Global | hdis-\<App-Name\>-\<Umgebung\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissionen-entw </li></ul>  |
| Azure HDInsight: Hadoop        | Global | hdihd-\<App-Name\>-\<Umgebung\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissionen-entw</li></ul>    |
| Azure HDInsight: R Server      | Global | hdir-\<App-Name\>-\<Umgebung\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissionen-entw</li></ul>   |
| Azure HDInsight: HBase         | Global | hdihb-\<App-Name\>-\<Umgebung\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissionen-entw</li></ul> |
| Power BI Embedded         | Global | pbiemb\<App-Name\>\<Umgebung\>  | <ul><li>pbiem-navigator-prod </li><li>pbiem-emissionen-entw</li></ul> |

### <a name="internet-of-things-iot"></a>Internet der Dinge (IoT, Internet of Things)

| Ressourcentyp                         | `Scope`          | Format                             | Beispiele                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics auf IoT Edge | Resource group | asa-\<App-Name\>-\<Umgebung\>   | <ul><li>asa-navigator-prod </li><li>asa-emissionen-entw</li></ul>     |
| Azure IoT Hub                      | Global         | aih-\<App-Name\>-\<Umgebung\>   | <ul><li>aih-navigator-prod </li><li>aih-emissionen-entw</li></ul>     |
| Azure Event Hubs                          | Global         | evh-\<App-Name\>-\<Umgebung\>   | <ul><li>evh-navigator-prod </li><li>anh-emissionen-entw</li></ul>     |
| Azure Notification Hubs                   | Resource group | anh-\<App-Name\>-\<Umgebung\>   | <ul><li>anh-navigator-prod </li><li>anh-emissionen-entw</li></ul>     |
| Azure Notification Hubs-Namespace         | Global         | anhns-\<App-Name\>-\<Umgebung\> | <ul><li>anhns-navigator-prod </li><li>anhns-emissionen-entw</li></ul> |
