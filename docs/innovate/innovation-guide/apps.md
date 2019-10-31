---
title: 'Azure-Innovationsleitfaden: Interagieren über Apps'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Informieren Sie sich über Innovation durch Interagieren über Apps mithilfe von Azure.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: df91d44d9b1efc2196b8b322c247dd39ef3d0d1e
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769357"
---
::: zone target="docs"

# <a name="azure-innovation-guide-engage-through-apps"></a>Azure-Innovationsleitfaden: Interagieren über Apps

::: zone-end

::: zone target="chromeless"

# <a name="engage-through-apps"></a>Interagieren über Apps

::: zone-end

Innovation mit Apps umfasst sowohl die Modernisierung Ihrer vorhandenen Apps, die lokal gehostet werden, als auch die Erstellung von cloudnativen Apps mithilfe von Containern oder serverlosen Technologien. Bei der App-Modernisierung bietet Azure PaaS-Dienste wie Azure App Service, um die vorhandenen Web- und API-Apps, die zur Bereitstellung in Azure in .NET, .NET Core, Java, Node.js, Ruby, Python oder PHP geschrieben wurden, problemlos zu modernisieren. Mit einem Open-Standard-Containermodell ist das Erstellen von Microservices oder das Containerisieren Ihrer vorhandenen Anwendungen sowie deren Bereitstellung in Azure mithilfe verwalteter Diensten wie Azure Kubernetes Services, Azure Container Instances und Web-App für Container ganz einfach. Serverlose Technologien wie Azure Functions und Azure Logic Apps helfen Ihnen, sich auf das Erstellen Ihrer Anwendung mit einem Verbrauchsmodell (Sie bezahlen für das, was Sie nutzen) statt auf die Bereitstellung und Verwaltung der Infrastruktur zu konzentrieren.

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-fastertabdelivervaluefaster"></a>[Schnelleres Liefern von Ergebnissen](#tab/DeliverValueFaster)

Einer der Vorteile von cloudbasierten Lösungen ist die Möglichkeit, Feedback schneller zu sammeln und Ihren Endbenutzern Ergebnisse zu liefern. Unabhängig davon, ob es sich bei dem Endbenutzer um einen externen Kunden oder einen Benutzer in Ihrem eigenen Unternehmen handelt, je schneller Sie Feedback zu Ihren Anwendungen erhalten, desto besser.

## <a name="azure-app-service"></a>Azure App Service

Azure App Service bietet eine Hostingumgebung für Ihre Anwendungen, durch die Infrastrukturverwaltung und Betriebssystempatching unnötig werden. Dieser Dienst ermöglicht eine automatisierte Skalierung, um die Anforderungen Ihrer Benutzer zu erfüllen, bei gleichzeitiger Bindung an von Ihnen definierte Grenzen, um die Kosten in Schach zu halten.

Azure App Service bietet erstklassige Unterstützung für Sprachen wir ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP oder Python. Wenn Sie einen anderen Laufzeitstapel hosten müssen, können Sie mit Web-App für Container schnell und einfach einen Docker-Container innerhalb der Azure App Service-Umgebung hosten und so Ihren benutzerdefinierten Codestapel in einer Umgebung hosten, die Ihnen den Umgang mit Servern erspart.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure App Service-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **App Services**.
2. Konfigurieren eines neuen Diensts: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste der gehosteten Anwendungen die gewünschte App aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Mit Azure Cognitive Services können Sie erweiterte intelligente Funktionen direkt in Ihre Anwendung einbringen, und zwar über eine Reihe von APIs, mit denen Sie die von Microsoft unterstützten KI- und Machine Learning-Algorithmen nutzen können.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Cognitive Service-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Cognitive Services**.
2. Konfigurieren eines neuen Diensts: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste der gehosteten Dienste den gewünschten Dienst aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-services"></a>Azure Bot Services

Azure Bot Services erweitern Ihre Standardanwendung um eine natürliche Bot-Schnittstelle, die KI und Machine Learning nutzt, um eine neue Interaktion für Ihre Kunden zu schaffen.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Bot Services-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Botdienste**.
2. Konfigurieren eines neuen Diensts: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste der gehosteten Dienste den gewünschten Bot aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FbotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

Ihr Weg der Innovation wird letztendlich in Richtung DevOps führen. Microsoft verfügt bereits seit langem über ein lokales Produkt mit der Bezeichnung Team Foundation Server (TFS). Auf unserem eigenen Weg der Innovation haben wir Azure DevOps als cloudbasierten Dienst zur Bereitstellung von Build- und Releasetools entwickelt, die viele verschiedene Sprachen und Ziele für Ihre Releases unterstützen. [Azure DevOps](https://docs.microsoft.com/azure/devops)

## <a name="visual-studio-app-center"></a>Visual Studio App Center

Da mobile Apps immer beliebter werden, wächst die Notwendigkeit einer Plattform, die automatisierte Tests auf realen Geräten verschiedener Konfigurationen ermöglicht. Visual Studio App Center bietet nicht nur einen Ort, an dem Sie Ihre Anwendungen übergreifend für iOS, Android, Windows und macOS testen können, sondern bietet auch eine Überwachungsplattform mit der Möglichkeit, Azure Application Insights zu nutzen, um schnell und einfach Rückschlüsse aus Ihren Telemetriedaten zu ziehen. Weitere Informationen finden Sie in der [Übersicht zu Visual Studio App Center](https://docs.microsoft.com/appcenter).

Visual Studio App Center bietet auch einen Benachrichtigungsdienst, bei dem mit einem einzelnen Aufruf plattformübergreifend Benachrichtigungen an Ihre Anwendung gesendet werden können, ohne dass jeder Benachrichtigungsdienst einzeln kontaktiert werden muss. Weitere Informationen finden Sie unter [Visual Studio App Center Push (ACP)](https://docs.microsoft.com/appcenter/push).

### <a name="read-more"></a>Weitere Informationen

- [App Service: Übersicht](https://docs.microsoft.com/azure/app-service/overview)
- [Web-Apps für Container: Ausführen eines benutzerdefinierten Containers](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [Einführung in Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Azure für .NET- und .NET Core-Entwickler](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Dokumentation für das Azure-SDK für Python](https://docs.microsoft.com/azure/python)
- [Azure für Java-Cloudentwickler](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Erstellen einer PHP-Web-App in Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Dokumentation für das Azure SDK für JavaScript](https://docs.microsoft.com/azure/javascript)
- [Dokumentation für das Azure SDK für Go](https://docs.microsoft.com/azure/go)
- [DevOps-Lösungen](https://azure.microsoft.com/solutions/devops)

# <a name="cloud-native-appstabcloudnative"></a>[Cloudnative Apps](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>Was sind cloudnative Anwendungen?

Cloudnative Anwendungen sind prinzipell auf die Cloudskalierung und Leistung ausgerichtet. Sie sind basierend auf Microservicesarchitekturen lose gekoppelt, verwenden verwaltete Dienste, können beobachtet werden und nutzen Continuous Delivery-Prozesse, um Zuverlässigkeit und eine kürzere Markteinführungszeit zu gewährleisten. Im Allgemeinen sind sie portabel und können in dynamischen Umgebungen wie öffentlichen, privaten und hybriden Clouds ausgeführt werden. Cloudnative Anwendungen werden in der Regel mithilfe einer oder mehrerer der folgenden Methoden erstellt:

- Microservices
- Serverlos
- Container

## <a name="microservices"></a>Microservices

Microservices sind ein Architekturstil für Software. Anwendungen bestehen darin aus kleinen, unabhängigen Modulen, die miteinander über gut definierte API-Verträge kommunizieren. Diese Dienstmodule sind hochgradig entkoppelte Bausteine, die klein genug sind, um eine einzelne Funktionalität zu implementieren. Microservices bieten Ihnen folgende Möglichkeiten:

- Unabhängiges Erstellen von Diensten
- Autonomes Skalieren von Diensten
- Verwenden der am besten geeigneten Methoden für Bereitstellung und Programmiersprache
- Isolieren von Fehlerquellen
- Schnelleres Liefern von Ergebnissen

### <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

Nutzen Sie einen vollständig verwalteten Kubernetes-Dienst, um die Bereitstellung, das Upgrade und die Skalierung von Clusterressourcen bei Bedarf zu verwalten. AKS vereinfacht die Bereitstellung und Verwaltung von containerbasierten Anwendungen. Der Dienst umfasst die serverlose Plattform Kubernetes, integrierte CI/CD-Funktionen (Continuous Integration/Continuous Delivery) sowie Sicherheit und Governance auf Unternehmensniveau. Ihre Entwicklungs- und Betriebsteams können gemeinsam auf einer Plattform arbeiten, um Anwendungen ohne Bedenken schnell erstellen, ausliefern und skalieren zu können.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Kubernetes Services gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Kubernetes-Dienste**.
2. Konfigurieren eines neuen Diensts: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten eines vorhandenen Diensts: Wählen Sie den gewünschten Kubernetes-Dienst aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters]" submitText="Go to Kubernetes Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>Ereignisbasierte Lösungen

### <a name="azure-functions"></a>Azure Functions

Azure Functions bietet eine Plattform zum Ausführen kleiner Codeelemente oder Funktionen in der Cloud. Functions kann eine Möglichkeit sein, mit dem Umgestalten Ihres Codes in eine Microservicearchitektur zu beginnen.

Die Azure Functions-Runtime unterstützt viele Sprachen, einschließlich C#, Java, JavaScript und Python. Eine vollständige Auflistung finden Sie unter [In Azure Functions unterstützte Sprachen](https://docs.microsoft.com/azure/azure-functions/supported-languages).

Ein weiterer Vorteil von Functions ist die Möglichkeit, durch unterschiedliche Aktionen und Ereignisse wie HTTPTriggers, TimerTriggers und Trigger aus anderen Azure-Diensten wie Blob Storage, EventGrid und ServiceBus ausgelöst zu werden. Weitere Informationen zu Triggern und Bindungen finden Sie unter [Konzepte für Azure Functions-Trigger und -Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Functions-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Funktions-App**.
2. Konfigurieren einer neuen App: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Apps: Wählen Sie in der Liste der Funktions-Apps die gewünschte App aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>Serverlose Lösungen

Erstellen Sie cloudnative Apps mithilfe einer vollständig verwalteten Plattform, die die Skalierung, Verfügbarkeit und Leistung für Sie verwaltet, ohne dass Sie Infrastruktur bereitstellen und verwalten müssen. Vorteile serverloser Lösungen von Azure sind unter anderem:

- Höhere Entwicklergeschwindigkeit
- Optimieren der Teamleistung
- Optimieren der Auswirkungen auf das Unternehmen

### <a name="azure-logic-apps"></a>Azure Logic Apps

Integrieren Sie Daten und Apps, anstatt komplexen Integrationscode zwischen sehr unterschiedlichen Systemen zu schreiben. Erstellen Sie serverlose Workflows visuell mithilfe von Azure Logic Apps, und verwenden Sie Ihre eigenen APIs, serverlosen Funktionen oder vorkonfigurierten Software-as-a-Service-Connectors (SaaS), einschließlich Salesforce, Microsoft Office 365 und Dropbox.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Logic Apps gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Logic Apps**.
2. Konfigurieren einer neuen App: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Apps: Wählen Sie die gewünschte Logik-App aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2Fworkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>Serverlose API-Verwaltung

Veröffentlichen, schützen, transformieren, verwalten und überwachen Sie APIs mit Azure API Management, einem vollständig verwalteten Dienst, der ein Nutzungsmodell beinhaltet, das für serverlose Anwendungen optimal entwickelt und implementiert wurde.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von API Management-Diensten gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienste**.
2. Konfigurieren eines neuen Diensts: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten eines vorhandenen Diensts: Wählen Sie den gewünschten Dienst aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Container

Wenn es um die Modernisierung Ihres Anwendungsportfolios geht, bietet Azure verschiedene Containerdienste zum Migrieren Ihrer vorhandenen Anwendungen per Lift & Shift in Container sowie zum Erstellen cloudnativer Microserviceanwendungen, um Ihren Benutzern schneller Ergebnisse zu liefern. Verwenden Sie umfassende Entwickler- und CI/CD-Tools zum Entwickeln, Aktualisieren und Verwalten Ihrer containerbasierten Anwendungen. Verwalten Sie Container bedarfsorientiert mit einem vollständig verwalteten Orchestrierungsdienst für Kubernetes-Container, der in Azure Active Directory integriert ist. Unabhängig davon, an welchem Punkt der App-Modernisierung Sie sich befinden, beschleunigen Sie Ihre Entwicklung containerbasierter Anwendungen, und erfüllen Sie gleichzeitig Ihre Sicherheitsanforderungen.

### <a name="azure-container-instances"></a>Azure Container Instances

Bedarfsgesteuertes Ausführen von Docker-Containern in einer verwalteten, serverlosen Azure-Umgebung. Azure Container Instances (ACI) ist eine Lösung für alle Szenarien, die in isolierten Containern ohne Orchestrierung betrieben werden können. Durch die Ausführung Ihrer Workloads in ACI können Sie sich auf den Entwurf und die Erstellung Ihrer Anwendungen konzentrieren, statt die zugrundeliegende Infrastruktur verwalten zu müssen.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Container Instances gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Containerinstanzen**.
2. Konfigurieren einer neuen Containerinstanz: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Containerinstanzen: Wählen Sie die gewünschte Containerinstanz aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FcontainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Azure Red Hat OpenShift bietet flexible Self-Service-Bereitstellung vollständig verwalteter OpenShift-Cluster. Halten Sie gesetzliche Bestimmungen ein, und konzentrieren Sie sich auf die Entwicklung Ihrer Anwendungen, während die Master-, Infrastruktur- und Anwendungsknoten sowohl von Microsoft als auch von Red Hat gepatcht, aktualisiert und überwacht werden. Wählen Sie für Registrierung, Netzwerk, Speicher oder CI/CD eigene Lösungen aus, oder beginnen Sie rasch mit der Verwendung integrierter Lösungen mit automatischer Quellcodeverwaltung, Container- und Anwendungsbuilds, Bereitstellungen, Skalierung, Health Management und vielem mehr.

**Navigieren zu [Azure Red Hat OpenShift](https://docs.microsoft.com/azure/openshift/intro-openshift)**

# <a name="isolate-points-of-failuretabisolatepointsoffailure"></a>[Isolieren von Fehlerquellen](#tab/IsolatePointsOfFailure)

Beim Übergang aus der anfänglichen Testphase sollten Sie Möglichkeiten zum Isolieren und Beheben von Fehlerquellen prüfen. Aufgrund der gegebenen Verteilung in der Azure-Cloud können Sie Ihre Anwendung so gestalten, dass Fehler minimiert und gleichzeitig die Leistung verbessert wird.

## <a name="azure-front-door"></a>Azure Front Door

Azure Front Door bietet einen skalierbaren, sicheren Einstiegspunkt für die weltweite Bereitstellung Ihrer Anwendung. Azure Front Door kombiniert die Optimierung des Datenverkehrs für optimale Leistung und sofortiges globales Failover. Azure Front Door sollte gegenüber Traffic Manager bevorzugt werden, wenn eine Beendigung der Transport Layer Security-Protokollierung (SSL-Auslagerung) oder eine Verarbeitung der Anwendungsschicht pro HTTP/HTTPS-Anforderung benötigt wird.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Frontdoor-Instanzen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Frontdoor-Instanzen**.
2. Konfigurieren einer neuen Frontdoor-Instanz: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Frontdoor-Instanzen: Wählen Sie die gewünschte Frontdoor-Instanz aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ffrontdoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Traffic Manager

Traffic Manager bietet einen DNS-basierten Lastenausgleich, der basierend auf verschiedenen Regeln weitergeleitet werden kann. Dadurch wird Resilienz bei Ausfall bereitgestellter Dienste gewährleistet. Sie können Traffic Manager auch stapeln, damit sowohl fehlerbasiertes als auch leistungsbasiertes Routing verwendet werden kann, um bestmögliche Leistung basierend auf der Geografie zu bieten.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Traffic Manager-Profilen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Traffic Manager-Profile**.
2. Konfigurieren eines neuen Profils: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Profile: Wählen Sie das gewünschte Profil aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ftrafficmanagerprofiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Azure bietet ein verteiltes Content Delivery Network (CDN), mit dem Sie die zeitnahe Bereitstellung von Inhalten sicherstellen können, indem Sie diese in der Nähe Ihrer Endbenutzer zwischenspeichern. Diese Zwischenspeicherung trägt dazu bei, das Erlebnis für Ihre Kunden zu verbessern, und verhindert Probleme beim Herunterladen von Inhalten, die durch Netzwerkprobleme zwischen dem CDN-Endpunkt und dem Rechenzentrum, das Ihre Anwendung hostet, verursacht werden. Dieses CDN kann auch von nicht in Azure gehosteten Anwendungen verwendet werden.

### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von CDN-Profilen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **CDN-Profile**.
2. Konfigurieren eines neuen Profils: Klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen.
3. Verwalten vorhandener Profile: Wählen Sie das gewünschte Profil aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.cdn%2Fprofiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="read-more"></a>Weitere Informationen

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)
- [Content Delivery Network](https://docs.microsoft.com/azure/cdn)
