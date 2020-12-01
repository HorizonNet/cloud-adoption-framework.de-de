---
title: 'Azure-Innovation: Interagieren über Anwendungen'
description: In diesem Artikel erfahren Sie mehr über Azure-Dienste, die Sie dabei unterstützen, Ihre vorhandenen Web- und API-Apps mühelos zu modernisieren und cloudnative Anwendungen zu erstellen.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 922a123fe13b268548e2b51ffcc9d42c05d9c64a
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94880839"
---
# <a name="engage-customers-through-applications"></a>Einbinden von Kunden durch Anwendungen

Innovation mit Anwendungen umfasst sowohl die Modernisierung Ihrer vorhandenen Anwendungen, die lokal gehostet werden, als auch die Erstellung von cloudnativen Anwendungen mithilfe von Containern oder serverlosen Technologien. Azure bietet PaaS-Dienste wie Azure App Service, um die vorhandenen Web- und API-Apps, die zur Bereitstellung in Azure in .NET, .NET Core, Java, Node.js, Ruby, Python oder PHP geschrieben wurden, problemlos zu modernisieren.

Mit einem Open-Standard-Containermodell ist das Erstellen von Microservices oder das Containerisieren Ihrer vorhandenen Anwendungen sowie deren Bereitstellung in Azure mithilfe verwalteter Diensten wie Azure Kubernetes Service, Azure Container Instances und Web-App für Container ganz einfach. Serverlose Technologien wie Azure Functions und Azure Logic Apps verwenden ein Verbrauchsmodell (Sie bezahlen für das, was Sie nutzen) und helfen Ihnen, sich auf die Erstellung Ihrer Anwendung zu konzentrieren, anstatt die Infrastruktur bereitzustellen und zu verwalten.

## <a name="deliver-value-faster"></a>[Schnelleres Liefern von Ergebnissen](#tab/DeliverValueFaster)

Einer der Vorteile von cloudbasierten Lösungen ist die Möglichkeit, Feedback schneller zu sammeln und Ihren Benutzern Ergebnisse zu liefern. Unabhängig davon, ob es sich bei dem Benutzer um einen externen Kunden oder einen Benutzer in Ihrem eigenen Unternehmen handelt, je schneller Sie Feedback zu Ihren Anwendungen erhalten, desto besser.

### <a name="azure-app-service"></a>Azure App Service

Azure App Service bietet eine Hostingumgebung für Ihre Anwendungen, durch die Infrastrukturverwaltung und Betriebssystempatching unnötig werden. Dieser Dienst ermöglicht eine automatisierte Skalierung, um die Anforderungen Ihrer Benutzer zu erfüllen, bei gleichzeitiger Bindung an von Ihnen definierte Grenzen, um die Kosten in Schach zu halten.

Azure App Service bietet erstklassige Unterstützung für Sprachen wir ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP und Python. Wenn Sie einen anderen Laufzeitstapel hosten müssen, können Sie mit Web-App für Container schnell und einfach einen Docker-Container innerhalb von App Service hosten und so Ihren benutzerdefinierten Codestapel in einer Umgebung hosten, die Ihnen den Umgang mit Servern erspart.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure App Service-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **App Services**.
2. Einen neuen Dienst konfigurieren: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Vorhandene Dienste verwalten: Wählen Sie die gewünschte Anwendung aus der Liste der gehosteten Anwendungen aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2FSites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-cognitive-services"></a>Azure Cognitive Services

Mit Azure Cognitive Services können Sie erweiterte intelligente Funktionen direkt in Ihre Anwendung einbringen, und zwar über eine Reihe von APIs, mit denen Sie die von Microsoft unterstützten KI- und Machine Learning-Algorithmen nutzen können.

<!-- markdownlint-disable MD024 -->

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Cognitive Service-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Cognitive Services**.
2. Einen neuen Dienst konfigurieren: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste der gehosteten Dienste den gewünschten Dienst aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-bot-service"></a>Azure Bot Service

Azure Bot Services erweitern Ihre Standardanwendung durch das Hinzufügen einer natürlichen Bot-Schnittstelle, die KI und Machine Learning nutzt, um eine neue Möglichkeit der Interaktion mit Ihren Kunden zu schaffen.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Bot Service-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Botdienste**.
2. Einen neuen Dienst konfigurieren: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Dienste: Wählen Sie den gewünschten Bot aus der Liste der gehosteten Dienste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-devops"></a>Azure DevOps

Ihr Weg der Innovation wird letztendlich in Richtung DevOps führen. Microsoft verfügt bereits seit langem über ein lokales Produkt mit der Bezeichnung Team Foundation Server (TFS). Auf unserem eigenen Weg der Innovation haben wir Azure DevOps als cloudbasierten Dienst zur Bereitstellung von Build- und Releasetools entwickelt, die viele Sprachen und Ziele für Ihre Releases unterstützen. Weitere Informationen finden Sie unter [Azure DevOps](/azure/devops).

### <a name="visual-studio-app-center"></a>Visual Studio App Center

Da mobile Apps immer beliebter werden, wächst die Notwendigkeit einer Plattform, die automatisierte Tests auf realen Geräten verschiedener Konfigurationen ermöglicht. Visual Studio App Center bietet nicht nur einen Ort, an dem Sie Ihre Anwendungen übergreifend für iOS, Android, Windows und macOS testen können, sondern bietet auch eine Überwachungsplattform, die Azure Application Insights nutzen kann, um Ihre Telemetriedaten schnell und einfach zu analysieren. Weitere Informationen finden Sie unter [Visual Studio App Center](/appcenter).

Visual Studio App Center bietet auch einen Benachrichtigungsdienst, mit dem Sie mit einem einzelnen Aufruf plattformübergreifend Benachrichtigungen an Ihre Anwendung senden können, ohne dass jeder Benachrichtigungsdienst einzeln kontaktiert werden muss. Weitere Informationen finden Sie unter [Visual Studio App Center Push (ACP)](/appcenter/push).

### <a name="learn-more"></a>Weitere Informationen

- [App Service: Übersicht](/azure/app-service/overview)
- [Web-App für Container: Ausführen eines benutzerdefinierten Containers](/azure/app-service/containers/quickstart-docker)
- [Einführung in Azure Functions](/azure/azure-functions/functions-overview)
- [Azure für .NET- und .NET Core-Entwickler](/dotnet/azure/?view=azure-dotnet)
- [Dokumentation für das Azure-SDK für Python](/azure/python)
- [Azure für Java-Cloudentwickler](/azure/java/?view=azure-java-stable)
- [Erstellen einer PHP-Web-App in Azure](/azure/app-service/app-service-web-get-started-php)
- [Dokumentation für das Azure SDK für JavaScript](/azure/javascript)
- [Dokumentation für das Azure SDK für Go](/azure/go)
- [DevOps-Lösungen](https://azure.microsoft.com/solutions/devops)

## <a name="create-cloud-native-applications"></a>[Erstellen cloudnativer Anwendungen](#tab/CloudNative)

### <a name="what-are-cloud-native-applications"></a>Was sind cloudnative Anwendungen?

Cloudnative Anwendungen sind prinzipell auf die Cloudskalierung und Leistung ausgerichtet. Sie sind basierend auf Microservicesarchitekturen lose gekoppelt, verwenden verwaltete Dienste, können beobachtet werden und nutzen Continuous Delivery-Prozesse, um Zuverlässigkeit und eine kürzere Markteinführungszeit zu gewährleisten. In der Regel sind sie portabel und können in dynamischen Umgebungen wie öffentlichen, privaten und hybriden Clouds ausgeführt werden. Cloudnative Anwendungen werden im Allgemeinen mit mindestens einem der folgenden Ansätze erstellt:

- Microservices
- Serverlos
- Container

### <a name="microservices"></a>Microservices

Microservices sind ein Architekturstil für Software. Anwendungen bestehen darin aus kleinen, unabhängigen Modulen, die miteinander über gut definierte API-Verträge kommunizieren. Diese Dienstmodule sind hochgradig entkoppelte Bausteine, die klein genug sind, um eine einzelne Funktionalität zu implementieren. Microservices bieten Ihnen folgende Möglichkeiten:

- Unabhängiges Erstellen von Diensten
- Autonomes Skalieren von Diensten
- Verwenden der am besten geeigneten Methoden für Bereitstellung und Programmiersprachen.
- Isolieren von Fehlerquellen
- Schnelleres Liefern von Ergebnissen

### <a name="microservices-azure-kubernetes-service-aks"></a>Microservices: Azure Kubernetes Service (AKS)

Nutzen Sie einen vollständig verwalteten Kubernetes-Dienst, um die Bereitstellung, das Upgrade und die Skalierung von Clusterressourcen bei Bedarf zu verwalten. AKS vereinfacht die Bereitstellung und Verwaltung von containerbasierten Anwendungen. Der Dienst umfasst die serverlose Plattform Kubernetes, integrierte CI/CD-Funktionen (Continuous Integration/Continuous Delivery) sowie Sicherheit und Governance auf Unternehmensniveau. Ihre Entwicklungs- und Betriebsteams können gemeinsam auf einer Plattform arbeiten, um Anwendungen ohne Bedenken schnell erstellen, ausliefern und skalieren zu können.

#### <a name="action"></a>Aktion

So konfigurieren oder überwachen Sie einen AKS-Dienst

1. Navigieren Sie zu **Azure Kubernetes Service**.
2. Einen neuen Dienst konfigurieren: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste den gewünschten Kubernetes-Dienst aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FManagedClusters]" submitText="Go to Azure Kubernetes Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-solutions"></a>Serverlose Lösungen

Erstellen Sie cloudnative Anwendungen mithilfe einer vollständig verwalteten Plattform, die die Skalierung, Verfügbarkeit und Leistung für Sie verwaltet, ohne dass Sie Infrastruktur bereitstellen und verwalten müssen. Vorteile serverloser Lösungen von Azure sind unter anderem:

- Höhere Entwicklergeschwindigkeit.
- Optimieren der Teamleistung.
- Optimieren der Auswirkungen auf das Unternehmen.

### <a name="serverless-solutions-azure-functions"></a>Serverlose Lösungen: Azure-Funktionen

Azure Functions bietet eine Plattform zum Ausführen kleiner Codeeinheiten oder Funktionen in der Cloud. Functions kann eine Möglichkeit sein, mit dem Umgestalten Ihres Codes in eine Microservicearchitektur zu beginnen.

Die Azure Functions-Runtime unterstützt viele Sprachen, einschließlich C#, Java, JavaScript und Python. Eine vollständige Liste finden Sie unter [In Azure Functions unterstützte Sprachen](/azure/azure-functions/supported-languages).

Ein weiterer Vorteil von Functions ist die Möglichkeit, dass die Funktionen durch unterschiedliche Aktionen und Ereignisse wie HTTP-Trigger, Trigger mit Timer und Trigger aus anderen Azure-Diensten wie Blob Storage, Event Grid und Service Bus ausgelöst werden können. Weitere Informationen zu Triggern und Bindungen finden Sie unter [Konzepte für Azure Functions-Trigger und -Bindungen](/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Functions-Bereitstellungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Funktions-App**.
2. Konfigurieren einer neuen Funktions-App: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Funktions-Apps: Wählen Sie die gewünschte Funktions-App aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2FSites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-solutions-azure-logic-apps"></a>Serverlose Lösungen: Azure Logic Apps

Integrieren Sie Daten und Anwendungen, anstatt komplexen Integrationscode zwischen sehr unterschiedlichen Systemen zu schreiben. Erstellen Sie serverlose Workflows visuell mithilfe von Azure Logic Apps, und verwenden Sie Ihre eigenen APIs, serverlosen Funktionen oder vorkonfigurierten Software-as-a-Service-Connectors (SaaS), einschließlich Salesforce, Microsoft 365 und Dropbox.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure Logic Apps gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Logic Apps**.
2. Konfigurieren einer neuen Logik-App: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Logik-Apps: Wählen Sie die gewünschte Logik-App aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2FWorkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-solutions-api-management"></a>Serverlose Lösungen: API Management

Veröffentlichen, schützen, transformieren, verwalten und überwachen Sie APIs mit Azure API Management, einem vollständig verwalteten Dienst, der ein Nutzungsmodell beinhaltet, das für serverlose Anwendungen optimal entwickelt und implementiert wurde.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von API Management-Diensten gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienste**.
2. Einen neuen Dienst konfigurieren: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Dienste: Wählen Sie in der Liste den gewünschten Dienst aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2FService]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="containers"></a>Container

Für die Modernisierung Ihres Anwendungsportfolios bietet Azure verschiedene Containerdienste an, um Ihre vorhandenen Anwendungen zu Containern zu migrieren und cloudnative Microservicesanwendungen zu erstellen, damit Sie Ihren Benutzern schneller einen Mehrwert bieten können. Verwenden Sie umfassende Entwickler- und CI/CD-Tools zum Entwickeln, Aktualisieren und Verwalten Ihrer containerbasierten Anwendungen. Verwalten Sie Container bedarfsorientiert mit einem vollständig verwalteten Orchestrierungsdienst für Kubernetes-Container, der in Azure Active Directory integriert ist. Unabhängig davon, an welchem Punkt der Anwendungsmodernisierung Sie sich befinden, beschleunigen Sie Ihre Entwicklung containerbasierter Anwendungen, und erfüllen Sie gleichzeitig Ihre Sicherheitsanforderungen.

### <a name="containers-azure-container-instances"></a>Container: Azure Container Instances

Bedarfsgesteuertes Ausführen von Docker-Containern in einer verwalteten, serverlosen Azure-Umgebung. Azure Container Instances ist eine Lösung für alle Szenarien, die in isolierten Containern ohne Orchestrierung betrieben werden können. Wenn Sie Ihre Workloads in Containerinstanzen ausführen, können Sie sich auf den Entwurf und die Entwicklung Ihrer Anwendungen konzentrieren, statt die zugrundeliegende Infrastruktur verwalten zu müssen.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Containerinstanzen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Containerinstanzen**.
2. Konfigurieren einer neuen Containerinstanz: Wählen Sie **Hinzufügen** aus, und folgen Sie den Anweisungen.
3. Verwalten von vorhandenen Containerinstanzen: Wählen Sie die gewünschte Containerinstanz aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FContainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="containers-azure-red-hat-openshift"></a>Container: Azure Red Hat OpenShift

Azure Red Hat OpenShift bietet flexible Self-Service-Bereitstellung vollständig verwalteter OpenShift-Cluster. Halten Sie gesetzliche Bestimmungen ein, und konzentrieren Sie sich auf die Entwicklung Ihrer Anwendungen, während die Master-, Infrastruktur- und Anwendungsknoten sowohl von Microsoft als auch von Red Hat gepatcht, aktualisiert und überwacht werden. Wählen Sie Ihre eigenen Registrierungs-, Netzwerk-, Speicher- und CI/CD-Lösungen aus. Sie können sich auch für einen Schnelleinstieg entscheiden, indem Sie integrierte Lösungen mit automatisierter Quellcodeverwaltung, Container- und Anwendungsbuilds, Bereitstellungen, Skalierung und Integritätsverwaltung verwenden.

#### <a name="learn-more"></a>Weitere Informationen

- [Azure Red Hat OpenShift](/azure/openshift/intro-openshift)

## <a name="isolate-points-of-failure"></a>[Isolieren von Fehlerquellen](#tab/IsolatePointsOfFailure)

Beim Übergang aus der anfänglichen Testphase sollten Sie Möglichkeiten zum Isolieren und Beheben von Fehlerquellen prüfen. Aufgrund der verteilten Umgebung der Azure-Cloudplattform können Sie Ihre Anwendung so gestalten, dass Fehler minimiert werden und gleichzeitig die Leistung verbessert wird.

### <a name="azure-front-door"></a>Azure Front Door

Azure Front Door bietet einen skalierbaren, sicheren Einstiegspunkt, den Sie für die weltweite Bereitstellung Ihrer Anwendung nutzen können. Azure Front Door kombiniert die Optimierung des Datenverkehrs für optimale Leistung und sofortiges globales Failover. Azure Front Door sollte gegenüber Azure Traffic Manager bevorzugt werden, wenn eine Beendigung der TLS-Protokollierung (SSL-Auslagerung) oder eine Verarbeitung der Anwendungsschicht pro HTTP/HTTPS-Anforderung benötigt wird.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Front Door-Instanzen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Frontdoor-Instanzen**.
2. Konfigurieren einer neuen Front Door-Instanz: Wählen Sie **Hinzufügen** aus, und folgen Sie den Anweisungen.
3. Verwalten vorhandener Front Door-Instanzen: Wählen Sie die gewünschte Front Door-Instanz aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FFrontDoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="traffic-manager"></a>Traffic Manager

Traffic Manager bietet einen DNS-basierten Lastenausgleich, der basierend auf verschiedenen Regeln weitergeleitet werden kann. Durch diese Funktion wird Resilienz bei Ausfall bereitgestellter Dienste gewährleistet. Sie können Traffic Manager auch mit einer Stapelfunktion nutzen, damit sowohl fehlerbasiertes als auch leistungsbasiertes Routing verwendet werden kann, um bestmögliche Leistung basierend auf der Geografie zu bieten.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Traffic Manager-Profilen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Traffic Manager-Profile**.
2. Konfigurieren eines neuen Profils: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Profile: Wählen Sie das gewünschte Profil aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FTrafficManagerProfiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Azure bietet ein verteiltes Content Delivery Network (CDN), mit dem Sie die zeitnahe Bereitstellung von Inhalten sicherstellen können, indem Sie diese in der Nähe Ihrer Benutzer zwischenspeichern. Dieses Zwischenspeichern hilft, die Erfahrungen Ihrer Kunden zu verbessern. Beim Herunterladen von Inhalten werden auch Probleme vermieden, die durch Netzwerkprobleme verursacht werden, die zwischen dem CDN-Endpunkt und dem Rechenzentrum auftreten, das Ihre Anwendung hostet. Azure CDN kann auch von Anwendungen verwendet werden, die nicht in Azure gehostet werden.

#### <a name="action"></a>Aktion

Zum Konfigurieren oder Überwachen von Azure CDN-Profilen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **CDN-Profile**.
2. Konfigurieren eines neuen Profils: Wählen Sie **Hinzufügen** aus, und folgen Sie den Aufforderungen.
3. Verwalten vorhandener Profile: Wählen Sie das gewünschte Profil aus der Liste aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Cdn%2FProfiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Azure Front Door](/azure/frontdoor/front-door-overview)
- [Traffic Manager](/azure/traffic-manager)
- [Übersicht über das Azure Content Delivery Network (CDN)](/azure/cdn)
