---
title: Empfohlene Namens- und Kennzeichnungskonventionen
description: Enthält detaillierte Empfehlungen zur Benennung von Ressourcen und zur Kennzeichnung, die speziell auf die Unterstützung der Enterprise Cloud-Einführung ausgerichtet sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/05/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: 9c1377bfed389d435403f9f72dd6ac4e48ed8ee8
ms.sourcegitcommit: 8e5b670151cc8da0934037e23a1ef1609c6b2cc2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2020
ms.locfileid: "94378935"
---
<!-- docutune:disable -->
<!-- cSpell:ignore appcs arck cdnp cdne osdisk westeurope usgovia accountlookup messagequery -->

# <a name="recommended-naming-and-tagging-conventions"></a>Empfohlene Namens- und Kennzeichnungskonventionen

Organisieren Sie Ihre Cloudressourcen so, dass das operative Management und die Buchhaltungsanforderungen unterstützt werden. Gut definierte Namens- und Kennzeichnungskonventionen für Metadaten ermöglichen das schnelle Finden und Verwalten von Ressourcen. Diese Konventionen helfen auch dabei, Cloudnutzungskosten mithilfe von Mechanismen zur Rückbuchung und verbrauchsbasierter Kostenzuteilung an Geschäftsteams auszurichten.

Die genaue Darstellung und Benennung von Ressourcen ist für Sicherheitszwecke von entscheidender Bedeutung. Im Falle eines Sicherheitsvorfalls ist die schnelle Identifizierung der betroffenen Systeme, der potenziellen geschäftlichen Auswirkungen und der Art und Weise, wie sie verwendet werden, entscheidend für gute Risikoentscheidungen. Sicherheitsdienste wie [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-introduction) und [Azure Sentinel](https://docs.microsoft.com/azure/sentinel) verweisen auf Ressourcen und deren zugehörige Protokollierungs-/Warnungsinformationen nach Ressourcennamen.

Azure definiert [Benennungsregeln und -einschränkungen für Azure-Ressourcen](/azure/azure-resource-manager/management/resource-name-rules). Dieser Leitfaden enthält detaillierte Empfehlungen zur Unterstützung der Enterprise Cloud-Einführung.

Das Ändern von Ressourcennamen kann schwierig sein. Legen Sie eine umfassende Namenskonvention fest, bevor Sie mit einer größeren Cloudbereitstellung beginnen.

> [!NOTE]
> Jedes Unternehmen hat unterschiedliche Organisations-und Verwaltungsanforderungen. Die Empfehlungen dienen als Ausgangspunkt für Diskussionen in ihren Cloudeinführungsteams.
>
> Verwenden Sie im Verlauf dieser Diskussionen die folgende Vorlage, um die Namens- und Taggingentscheidungen zu erfassen, die Sie treffen, wenn Sie diese Empfehlungen an Ihre speziellen geschäftlichen Anforderungen anpassen.
>
> Laden Sie die [Vorlage zum Festhalten von Namens- und Kennzeichnungskonventionen](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/naming-and-tagging-conventions-tracking-template.xlsx) herunter.

## <a name="naming-and-tagging-resources"></a>Benennen und Kennzeichnen von Ressourcen

Eine Benennungs- und Kennzeichnungsstrategie beinhaltet geschäftliche und operative Details als Komponenten von Ressourcennamen und Metadatentags:

Mit der unternehmensbezogenen Seite dieser Strategie wird sichergestellt, dass Ressourcennamen und Tags die Organisationsinformationen enthalten, die zum Identifizieren der Teams benötigt werden. Verwenden Sie eine Ressource zusammen mit den Geschäftsbesitzern, die für die Ressourcenkosten verantwortlich sind.

Die operative Seite stellt sicher, dass Namen und Kennzeichnungen (Tags) Informationen enthalten, anhand denen IT-Teams die Workload, die Anwendung, die Umgebung, die Wichtigkeit und weitere Informationen erkennen können, die für die Verwaltung von Ressourcen nützlich sind.

## <a name="resource-naming"></a>Benennen von Ressourcen

In einer wirkungsvollen Namenskonvention werden Ressourcennamen aus wichtigen Ressourceninformationen als Namensbestandteilen zusammengesetzt. Werden beispielsweise die [empfohlenen Namenskonventionen](#example-names) verwendet, wird eine öffentliche IP-Ressource für eine SharePoint-Produktionsworkload wie folgt benannt: `pip-sharepoint-prod-westus-001`.

Anhand des Namens können Sie schnell den Typ der Ressource, deren zugehörige Workload, deren Bereitstellungsumgebung und die Azure-Region erkennen, in der sie gehostet wird.

### <a name="naming-scope"></a>Namensbereich

Alle Azure-Ressourcentypen weisen einen Bereich auf, der die Ebene definiert, auf der Ressourcennamen eindeutig sein müssen. Eine Ressource muss einen eindeutigen Namen innerhalb ihres Bereichs aufweisen.

Ein virtuelles Netzwerk hat beispielsweise einen Ressourcengruppenbereich, was bedeutet, dass es in einer bestimmten Ressourcengruppe nur ein Netzwerk namens `vnet-prod-westus-001` geben darf. Andere Ressourcengruppen können ein eigenes virtuelles Netzwerk mit dem Namen `vnet-prod-westus-001` aufweisen. Subnetze gehören in den Bereich eines virtuellen Netzwerks, daher muss jedes Subnetz innerhalb eines virtuellen Netzwerks eindeutig benannt sein.

Einige Ressourcennamen, etwa PaaS-Dienste mit öffentlichen Endpunkten oder DNS-Bezeichnungen virtueller Maschinen, haben globale Bereiche, was bedeutet, dass sie auf der gesamten Azure-Plattform eindeutig sein müssen.

Für Ressourcennamen gelten Längenbeschränkungen. Daher ist es wichtig, den Kontext, der in einen Namen eingebettet ist, mit dessen Bereich und Länge in Einklang zu bringen, wenn Sie Ihre Namenskonventionen entwickeln. Weitere Informationen finden Sie unter [Benennungsregeln und -einschränkungen für Azure-Ressourcen](/azure/azure-resource-manager/management/resource-name-rules).

### <a name="recommended-naming-components"></a>Empfohlene Namenskomponenten

Wenn Sie Ihre Namenskonvention erstellen, identifizieren Sie die wichtigsten Bestandteile der Informationen, die in einem Ressourcennamen berücksichtigt werden sollen. Unterschiedliche Informationen sind für unterschiedliche Ressourcentypen relevant. Die folgende Liste enthält Beispiele für Informationen, die beim Erstellen von Ressourcennamen nützlich sind.

Verwenden Sie möglichst kurze Namenskomponenten, um zu verhindern, dass die Längenbeschränkungen für Ressourcennamen überschritten werden.

| Namenskomponente            | BESCHREIBUNG                                                                                                                                                                                                      | Beispiele                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Geschäftseinheit               | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann diese Komponente ein einzelnes Organisationselement des Unternehmens auf oberster Ebene darstellen. | `fin`, `mktg`, `product`, `it`, `corp`           |
| Abonnementtyp           | Zusammenfassende Beschreibung des Zwecks des Abonnements, das die Ressource enthält. Häufig nach Umgebungstyp der Bereitstellung oder nach bestimmten Workloads aufgeschlüsselt.                                                       | `prod`, `shared`, `client`                       |
| Anwendungs- oder Dienstname | Der Name der Anwendung, der Workload oder des Diensts, zu der oder dem die Ressource gehört.                                                                                                                                    | `navigator`, `emissions`, `sharepoint`, `hadoop` |
| Bereitstellungsumgebung      | Die von der Ressource unterstützte Phase des Entwicklungslebenszyklus der Workload.                                                                                                                              | `prod`, `dev`, `qa`, `stage`, `test`             |
| Region                      | Die Azure-Region, in der die Ressource bereitgestellt wird.                                                                                                                                                                 | `westus`, `eastus2`, `westeurope`, `usgovia`     |

### <a name="recommended-resource-type-prefixes"></a>Empfohlene Präfixe für Ressourcentypen

Jede Workload kann aus vielen einzelne Ressourcen und Diensten bestehen. Ein Einbinden von Ressourcentyppräfixen in Ihre Ressourcennamen erleichtert die visuelle Erkennung von Anwendungs- oder Dienstkomponenten.

Diese Liste enthält empfohlene Azure-Ressourcentypenpräfixe, die Sie verwenden sollten, wenn Sie Ihre Namenskonventionen definieren.

<!-- cSpell:ignore apim snet traf vmss stvm arcm ntfns sqldb psql sqldw sqlstrdb ssimp srch hbase appi migr -->

### <a name="general"></a>Allgemein

| Ressourcentyp                      | Namenspräfix |
|---------------------------------|-------------|
| Verwaltungsgruppe                | mg-         |
| Resource group                  | rg-         |
| Richtliniendefinition               | policy-     |
| API Management-Dienstinstanz | apim-       |
| Verwaltete Identität                | id-         |

### <a name="networking"></a>Netzwerk

| Ressourcentyp                            | Namenspräfix |
|---------------------------------------|-------------|
| Virtuelles Netzwerk                       | vnet-       |
| Subnet                                | snet-       |
| Peering in virtuellen Netzwerken               | peer-       |
| Netzwerkschnittstelle (NIC)               | nic-        |
| Öffentliche IP-Adresse                     | pip-        |
| Lastenausgleich (intern)              | lbi-        |
| Lastenausgleich (extern)              | lbe-        |
| Netzwerksicherheitsgruppe (NSG)          | nsg-        |
| Anwendungssicherheitsgruppe (ASG)      | asg-        |
| Lokales Netzwerkgateway                 | lgw-        |
| Gateway des virtuellen Netzwerks               | vgw-        |
| VPN-Verbindung                        | cn-         |
| ExpressRoute-Verbindung                  | erc-        |
| Anwendungsgateway                   | agw-        |
| Routingtabelle                           | route-      |
| Benutzerdefinierte Route (User Defined Route, UDR)              | udr-        |
| Traffic Manager-Profil               | traf-       |
| Front Door                            | fd-         |
| CDN-Profil                           | cdnp-       |
| CDN-Endpunkt                          | cdne-       |
| Web Application Firewall-Richtlinie (WAF) | waf         |

### <a name="compute-and-web"></a>Compute und Web

| Ressourcentyp | Namenspräfix |
|--|--|
| Virtueller Computer | vm |
| VM-Skalierungsgruppe | vmss- |
| Verfügbarkeitsgruppe | avail- |
| Verwalteter Datenträger (Betriebssystem) | osdisk |
| Verwalteter Datenträger (Daten) | disk |
| VM-Speicherkonto | spvm |
| Server mit Azure Arc-Unterstützung: | arcs- |
| Kubernetes-Cluster mit Azure Arc-Unterstützung | arck |
| Containerregistrierung | cr |
| Containerinstanz | ci- |
| AKS-Cluster | aks- |
| Service Fabric-Cluster | sf- |
| App Service-Umgebung | ase- |
| App Service-Plan | plan- |
| Web-App | app- |
| Funktionen-App | func- |
| Clouddienst | cld- |
| Notification Hubs | ntf- |
| Notification Hubs-Namespace | ntfns- |

### <a name="databases"></a>Datenbanken

| Ressourcentyp                     | Namenspräfix |
|--------------------------------|-------------|
| Azure SQL-Datenbank-Server      | sql-        |
| Azure SQL-Datenbank             | sqldb-      |
| Azure Cosmos DB-Datenbank       | cosmos-     |
| Azure Cache for Redis-Instanz | redis-      |
| MySQL-Datenbank                 | mysql-      |
| PostgreSQL-Datenbank            | psql-       |
| Azure SQL Data Warehouse       | sqldw-      |
| Azure Synapse Analytics        | syn-        |
| SQL Server Stretch Database    | sqlstrdb-   |
| Verwaltete SQL-Instanz           | sqlmi-      |

### <a name="storage"></a>Storage

| Ressourcentyp               | Namenspräfix |
|--------------------------|-------------|
| Speicherkonto          | st          |
| Azure StorSimple         | ssimp       |
| Azure Container Registry | acr         |

### <a name="ai-and-machine-learning"></a>KI und maschinelles Lernen

| Ressourcentyp                       | Namenspräfix |
|----------------------------------|-------------|
| Azure Cognitive Search           | srch-       |
| Azure Cognitive Services         | cog-        |
| Azure Machine Learning-Arbeitsbereich | mlw-        |

### <a name="analytics-and-iot"></a>Analytics und IoT

| Ressourcentyp                       | Namenspräfix | |---------------------------------_|-------------| | Azure Analysis Services-Server   | as          | | Azure Databricks-Arbeitsbereich       | dbw-        | | Azure Stream Analytics           | asa-        | | Azure Data Explorer-Cluster      | dec         | | Azure Data Factory               | adf-        | | Data Lake Store-Konto          | dls         | | Data Lake Analytics-Konto      | dla         | | Event Hub                        | evh-        | | HDInsight – Hadoop-Cluster       | hadoop-     | | HDInsight – HBase-Cluster        | hbase-      | | HDInsight – Kafka-Cluster        | kafka-      | | HDInsight – Spark-Cluster        | spark-      | | HDInsight – Storm-Cluster        | storm-      | | HDInsight – ML Services-Cluster  | mls-        | | IoT Hub                          | iot-        | | Power BI Embedded                | pbi-        | | Time Series Insights-Umgebung | tsi-        |

### <a name="developer-tools"></a>Entwicklertools

| Ressourcentyp | Namenspräfix |
|---|---|
| App Configuration-Speicher | appcs- |

### <a name="integration"></a>Integration

| Ressourcentyp          | Namenspräfix |
|---------------------|-------------|
| Integrationskonto | ia-         |
| Logik-Apps          | logic-      |
| Service Bus         | sb-         |
| Service Bus-Warteschlange   | sbw-        |
| Service Bus-Topic   | sbt-        |

### <a name="management-and-governance"></a>Verwaltung und Governance

| Ressourcentyp | Namenspräfix |
|--|--|
| Automation-Konto | aa- |
| Azure Monitor-Aktionsgruppe | ag- |
| Blaupause | bp- |
| Blaupausenzuweisung | bpa- |
| Schlüsseltresor | kv- |
| Log Analytics-Arbeitsbereich | log- |
| Application Insights | appi- |
| Recovery Services-Tresor | rsv- |

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
| Anwendungsname          | Der Name der Anwendung, des Diensts oder der Workload, mit der die Ressource verknüpft ist.                                                                                                                                       | _ApplicationName_ | _{Anwendungsname}_                                               |
| Name der genehmigenden Person             | Die Person, die für das Genehmigen der Kosten zuständig ist, die mit dieser Ressource verbunden sind.                                                                                                                                                     | _Approver_        | _{E-Mail}_                                                  |
| Erforderliches/genehmigtes Budget  | Der Geldbetrag, der für diese Anwendung, diesen Dienst oder diese Workload zugeordnet ist.                                                                                                                                                          | _BudgetAmount_    | _{\$}_                                                     |
| Geschäftseinheit             | Oberste Abteilung Ihres Unternehmens, die Besitzer des Abonnements oder der Workload ist, zu dem oder der die Ressource gehört. In kleineren Unternehmen kann dieses Tag ein einzelnes Organisations- oder freigegebenes Element des Unternehmens auf oberster Ebene darstellen. | _BusinessUnit_    | _FINANZEN_ , _MARKETING_ , _{Produktname}_ , _CORP_ , _FREIGABE_ |
| Kostenstelle               | Buchhaltungskostenstelle, die dieser Ressource zugeordnet ist.                                                                                                                                                                | _CostCenter_      | _{Zahl}_                                                 |
| Notfallwiederherstellung         | Geschäftliche Bedeutung der Anwendung, Workload oder dieses Diensts.                                                                                                                                                       | _DR_              | _Unternehmenskritisch_ , _Kritisch_ , _Unverzichtbar_                |
| Enddatum des Projekts   | Datum, zu dem die Deaktivierung der Anwendung, Workload oder dieses Diensts geplant ist.                                                                                                                                         | _EndDate_         | _{Datum}_                                                   |
| Environment               | Bereitstellungsumgebung der Anwendung, Workload oder dieses Diensts.                                                                                                                                                     | _Env_             | _Prod_ , _Entw_ , _QA_ , _Stage_ , _Test_                       |
| Name des Besitzers                | Besitzer der Anwendung, der Workload oder des Diensts.                                                                                                                                                                      | _Besitzer_           | _{E-Mail}_                                                  |
| Name der anfordernden Person            | Der Benutzer, der die Erstellung dieser Anwendung angefordert hat.                                                                                                                                                                 | _Name der anfordernden Person_       | _{E-Mail}_                                                  |
| Dienstklasse             | Vereinbarung zum Servicelevel der Anwendung, der Workload oder des Diensts.                                                                                                                                              | _ServiceClass_    | _Dev_ , _Bronze_ , _Silver_ , _Gold_                          |
| Startdatum des Projekts | Datum, zu dem die Anwendung, Workload oder dieser Dienst erstmalig bereitgestellt wurde.                                                                                                                                                  | _StartDate_       | _{Datum}_                                                   |

## <a name="example-names"></a>Namensbeispiele

Der folgende Abschnitt enthält einige Namensbeispiele für häufige Azure-Ressourcentypen bei der Bereitstellung einer Unternehmenscloud.

<!-- TODO: Use tick marks for names. -->

<!-- cSpell:ignore mktgsharepoint acctlookupsvc vmhadoop vmtest vmsharepoint vmnavigator vmsqlnode stvmstcoreeastus stvmpmcoreeastus stvmstplmeastus stvmsthadoopeastus stnavigatordata stemissionsoutput stdiag stdiagsh ssimpnavigatorprod ssimpemissionsdev dlanavigatorprod dlsnavigatorprod dlaemissionsdev dlsemissionsdev weballow rdpallow sqlallow dnsblocked cloudapp azurewebsites servicebus appcn keda acrnavigatorprod -->

<!-- markdownlint-disable MD024 -->

### <a name="example-names-general"></a>Namensbeispiele: Allgemein

| Ressourcentyp                      | `Scope`                                 | Format                                                      | Beispiele                                                                                           |
|---------------------------------|---------------------------------------|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| Verwaltungsgruppe                | Geschäftseinheit und/oder Umgebungstyp | mg-\<Business Unit\>\[-\<Environment type\>\]               | <li> mg-mktg <li> mg-hr <li> mg-corp-prod <li> mg-fin-client                                       |
| Subscription                    | Account/ <br> Enterprise Agreement    | \<Business Unit\>-\<Subscription type\>-\<\#\#\#\>          | <li> mktg-prod-001 <li> konzern-freigabe-001 <li> fin-client-001                                        |
| Resource group                  | Subscription                          | rg-\<App or service name\>-\<Subscription type\>-\<\#\#\#\> | <li> rg-mktgsharepoint-prod-001 <li> rg-kontnachschldien-freigabe-001 <li> rg-ad-verz-dienste-freigabe-001 |
| API Management-Dienstinstanz | Global                                | apim-\<App or service name\>                                | apim-navigator-prod                                                                                |
| Verwaltete Identität                | Ressourcengruppe                        | id-\<App or service name\>                                  | id-appcn-keda-prod-eus-001                                                                         |

> [!NOTE]
> Die zuvor und anderswo in diesem Dokument verwendeten Beispielnamen verweisen auf eine dreistellige Zeichenauffüllung (\<\#\#\#\>). Das heißt,  mktg-prod- *001*
>
> Auffüllen unterstützt die Lesbarkeit für Menschen sowie das Sortieren von Ressourcen, wenn diese in einer Konfigurationsverwaltungs-Datenbank (CMDB), einem IT-Ressourcenverwaltungstool oder in herkömmlichen Buchhaltungstools verwaltet werden. Wenn die bereitgestellte Ressource als Teil eines größeren Bestands oder Portfolios von IT-Ressourcen zentral verwaltet wird, richtet sich der Ansatz des Auffüllens an Oberflächen aus, die diese Systeme zur Verwaltung des Bestands verwenden.
>
> Unglücklicherweise kann sich der herkömmliche Ansatz für die Ressourcenauffüllung in Infrastruktur-als-Code-Ansätzen als problematisch erweisen, bei denen möglicherweise Ressourcen basierend auf einer nicht aufgefüllten Zahl durchlaufen werden. Diese Vorgehensweise wird bei der Bereitstellung oder bei automatisierten Konfigurationsverwaltungsaufgaben häufig eingesetzt. Diese Skripts müssten routinemäßig die aufgefüllten Leerzeichen entfernen und die aufgefüllte Zahl in eine reelle Zahl konvertieren, wodurch Skriptentwicklung und Laufzeit verlangsamt werden.
>
> Die Methode, die Sie implementieren möchten, unterliegt Ihrer persönlichen Entscheidung. Das Auffüllen in diesem Artikel soll die Wichtigkeit der Verwendung eines konsistenten Ansatzes bei der Bestandsnummerierung veranschaulichen, nicht, welcher Ansatz überlegen ist. Bevor Sie sich für ein Zahlenschema (mit oder ohne Auffüllung) entscheiden, bewerten Sie, welche sich stärker auf langfristige Vorgänge auswirken: CMDB-/Ressourcenverwaltungslösungen oder codebasierte Bestandsverwaltung. Befolgen Sie dann konsistent die Auffülloption, die Ihren betrieblichen Anforderungen am besten entspricht.

### <a name="example-names-networking"></a>Namensbeispiele: Netzwerk

| Ressourcentyp                   | `Scope`           | Format                                                               | Beispiele                                                                                                                      |
|------------------------------|-----------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Virtuelles Netzwerk              | Resource group  | vnet-\<Subscription type\>-\<Region\>-\<\#\#\#\>                     | <li> vnet-freigabe-usaosten2-001 <li> vnet-prod-usawesten-001 <li> vnet-client-usaosten2-001 |
| Subnet                       | Virtuelles Netzwerk | snet-\<subscription\>-\<subregion\>-\<\#\#\#\>                       | <li> snet-freigabe-usaosten2-001 <li> snet-prod-usawesten-001 <li> snet-client-usaosten2-001 |
| Netzwerkschnittstelle (NIC)      | Resource group  | nic-\<\#\#\>-\<vm name\>-\<subscription\>-\<\#\#\#\>                   | <li> nic-01-dc1-freigabe-001 <li> nic-02-vmhadoop1-prod-001 <li> nic-02-vmtest1-client-001 |
| Öffentliche IP-Adresse            | Resource group  | pip-\<vm name or app name\>-\<Environment\>-\<subregion\>-\<\#\#\#\> | <li> pip-dc1-freigabe-usaosten2-001 <li> pip-hadoop-prod-usawesten-001 |
| Load Balancer                | Resource group  | lb-\<app name or role\>\<Environment\>\<\#\#\#\>                     | <li> lb-navigator-prod-001 <li> lb-sharepoint-entw-001 |
| Netzwerksicherheitsgruppe (NSG) | Subnetz oder NIC   | nsg-\<policy name or app name\>-\<\#\#\#\>                           | <li> nsg-weberlaub-001 <li> nsg-rdperlaub-001 <li> nsg-sqlerlaub-001 <li> nsg-dnsblocked-001 |
| Lokales Netzwerkgateway        | Virtuelles Gateway | lgw-\<Subscription type\>-\<Region\>-\<\#\#\#\>                      | <li> lgw-shared-eastus2-001 <li> lgw-prod-westus-001 <li> lgw-client-eastus2-001 |
| Gateway des virtuellen Netzwerks      | Virtuelles Netzwerk | vgw-\<Subscription type\>-\<Region\>-\<\#\#\#\>                      | <li> vgw-shared-eastus2-001 <li> vgw-prod-westus-001 <li> vgw-client-eastus2-001 |
| Standort-zu-Standort-Verbindung      | Resource group  | cn-\<local gateway name\>-to-\<virtual gateway name\>                | <li> cn-lgw-shared-eastus2-001-to-vgw-shared-eastus2-001 <li> cn-lgw-shared-eastus2-001-to-shared-westus-001 |
| VPN-Verbindung               | Resource group  | cn-\<subscription1\>\<region1\>-to-\<subscription2\>\<region2\>-     | <li> cn-freigabe-usaosten2-to-freigabe-usawesten <li> cn-prod-usaosten2-to-prod-usawesten |
| Routingtabelle                  | Resource group  | route-\<route table name\>                                           | <li> route-navigator <li> route-sharepoint |
| DNS-Bezeichnung                    | Global          | \<A record of vm\>.<region\>.cloudapp.azure.com                   | <li> dc1.usawesten.cloudapp.azure.com <li> web1.usaosten2.cloudapp.azure.com |

### <a name="example-names-compute-and-web"></a>Namensbeispiele: Compute und Web

| Ressourcentyp                  | `Scope`          | Format                                                              | Beispiele                                                                                                                          |
|-----------------------------|----------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Virtueller Computer             | Resource group | vm\<policy name or app name\>\<\#\#\#\>                              | <li> vmnavigator001 <li> vmsharepoint001 <li> vmsqlknoten001 <li> vmhadoop001 |
| VM-Speicherkonto          | Global         | stvm\<performance type\>\<app name or prod name\>\<region\>\<\#\#\#\> | <li> stvmstcoreusaosten2001 <li> stvmpmcoreusaosten2001 <li> stvmstplmusaosten2001 <li> stvmsthadoopusaosten2001 |
| Web-App                     | Global         | app-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{azurewebsites.net}]   | <li> app-navigator-prod-001.azurewebsites.net <li> app-accountlookup-dev-001.azurewebsites.net |
| Funktionen-App                | Global         | func-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{azurewebsites.net}]  | <li> func-navigator-prod-001.azurewebsites.net <li> func-accountlookup-dev-001.azurewebsites.net |
| Clouddienst               | Global         | cld-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{cloudapp.net}]        | <li> cld-navigator-prod-001.azurewebsites.net <li> cld-accountlookup-dev-001.azurewebsites.net |
| Notification Hub            | Resource group | ntf-\<App Name\>-\<Environment\>                                    | <li> ntf-navigator-prod <li> ntf-emissions-dev |
| Notification Hubs-Namespace | Global         | ntfns-\<App Name\>-\<Environment\>                                  | <li> ntfns-navigator-prod <li> ntfns-emissions-dev |

### <a name="example-names-databases"></a>Namensbeispiele: Datenbanken

| Ressourcentyp                     | `Scope`              | Format                                 | Beispiele                                                                  |
|--------------------------------|--------------------|----------------------------------------|---------------------------------------------------------------------------|
| Azure SQL-Datenbank-Server      | Global             | sql-\<App Name\>-\<Environment\>       | <li> sql-navigator-prod <li> sql-emissions-dev |
| Azure SQL-Datenbank             | Azure SQL-Datenbank | sqldb-\<Database Name>-\<Environment\> | <li> sqldb-users-prod <li> sqldb-users-dev |
| Azure Cosmos DB-Datenbank       | Global             | cosmos-\<App Name\>-\<Environment\>    | <li> cosmos-navigator-prod <li> cosmos-emissions-dev |
| Azure Cache for Redis-Instanz | Global             | redis-\<App Name\>-\<Environment\>     | <li> redis-navigator-prod <li> redis-emissionen-entw |
| MySQL-Datenbank                 | Global             | mysql-\<App Name\>-\<Environment\>     | <li> mysql-navigator-prod <li> mysql-emissionen-entw |
| PostgreSQL-Datenbank            | Global             | psql-\<App Name\>-\<Environment\>      | <li> psql-navigator-prod <li> psql-emissions-dev |
| Azure SQL Data Warehouse       | Global             | sqldw-\<App Name\>-\<Environment\>     | <li> sqldw-navigator-prod <li> sqldw-emissionen-entw |
| SQL Server Stretch Database    | Azure SQL-Datenbank | sqlstrdb-\<App Name\>-\<Environment\>  | <li> sqlstrdb-navigator-prod <li> sqlstrdb-emissionen-entw |

### <a name="example-names-storage"></a>Namensbeispiele: Storage

| Ressourcentyp                        | `Scope`  | Format                                                                        | Beispiele                                                              |
|-----------------------------------|--------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Speicherkonto (allgemeine Nutzung)     | Global | st\<storage name\>\<\#\#\#\>                                                  | <li> stnavigatordaten001 <li> stemissionenausgabe001 |
| Speicherkonto (Diagnoseprotokolle) | Global | stdiag\<first 2 letters of subscription name and number\>\<region\>\<\#\#\#\> | <li> stdiagsh001usaosten2001 <li> stdiagsh001usawesten001 |
| Azure StorSimple                  | Global | ssimp\<App Name\>\<Environment\>                                              | <li> ssimpnavigatorprod <li> ssimpemissionenentw |
| Azure Container Registry          | Global | acr\<App Name\>\<Environment\>\<\#\#\#\>                                      | <li> acrnavigatorprod001 |

### <a name="example-names-ai-and-machine-learning"></a>Namensbeispiele: KI und Machine Learning

| Ressourcentyp                       | `Scope`          | Format                            | Beispiele                                                          |
|----------------------------------|----------------|-----------------------------------|-------------------------------------------------------------------|
| Azure Cognitive Search           | Global         | srch-\<App Name\>-\<Environment\> | <li> srch-navigator-prod <li> srch-emissionen-entw |
| Azure Cognitive Services         | Resource group | cog-\<App Name\>-\<Environment\>  | <li> cog-navigator-prod <li> cog-emissions-dev |
| Azure Machine Learning-Arbeitsbereich | Resource group | mlw-\<App Name\>-\<Environment\>  | <li> mlw-navigator-prod <li> mlw-emissions-dev |

### <a name="example-names-analytics-and-iot"></a>Namensbeispiele: Analytics und IoT

| Ressourcentyp                  | `Scope`          | Format                              | Beispiele                                                              |
|-----------------------------|----------------|-------------------------------------|-----------------------------------------------------------------------|
| Azure Data Factory          | Global         | adf-\<App Name\>\<Environment\>     | <li> adf-navigator-prod <li> adf-emissions-dev |
| Azure Stream Analytics      | Resource group | asa-\<App Name\>-\<Environment\>    | <li> asa-navigator-prod <li> asa-emissionen-entw |
| Data Lake Analytics-Konto | Global         | dla\<App Name\>\<Environment\>      | <li> dlanavigatorprod <li> dlaemissionenentw |
| Data Lake Storage-Konto   | Global         | dls\<App Name\>\<Environment\>      | <li> dlsnavigatorprod <li> dlsemissionenentw |
| Event Hub                   | Global         | evh-\<App Name\>-\<Environment\>    | <li> anh-navigator-prod <li> anh-emissionen-entw |
| HDInsight: HBase-Cluster   | Global         | hbase-\<App Name\>-\<Environment\>  | <li> hbase-navigator-prod <li> hbase-emissions-dev |
| HDInsight: Hadoop-Cluster  | Global         | hadoop-\<App Name\>-\<Environment\> | <li> hadoop-navigator-prod <li> hadoop-emissions-dev |
| HDInsight: Spark-Cluster   | Global         | spark-\<App Name\>-\<Environment\>  | <li> spark-navigator-prod <li> spark-emissions-dev  |
| IoT Hub                     | Global         | iot-\<App Name\>-\<Environment\>    | <li> iot-navigator-prod <li> iot-emissions-dev |
| Power BI Embedded           | Global         | pbi-\<App Name\>\<Environment\>     | <li> pbi-navigator-prod <li> pbi-emissions-dev |

### <a name="example-names-integration"></a>Namensbeispiele: Integration

| Ressourcentyp        | `Scope`       | Format                                                     | Beispiele                                                      |
|-------------------|-------------|------------------------------------------------------------|---------------------------------------------------------------|
| Service Bus       | Global      | sb-\<App Name\>-\<Environment\>.[{servicebus.windows.net}] | <li> sb-navigator-prod <li> sb-emissionen-entw |
| Service Bus-Warteschlange | Service Bus | sbq-\<query descriptor\>                                   | <li> sbq-nachrabfrage |
| Service Bus-Topic | Service Bus | sbt-\<query descriptor\>                                   | <li> sbt-messagequery |
