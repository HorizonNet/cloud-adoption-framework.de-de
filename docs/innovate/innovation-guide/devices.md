---
title: 'Azure-Innovationsleitfaden: Interagieren über Geräte'
description: 'Azure-Innovationsleitfaden: Interagieren über Geräte'
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4744a1a019a8454f9a454c5eb75192a6d97b6998
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808310"
---
::: zone target="docs"

# <a name="azure-innovation-guide-interact-through-devices"></a>Azure-Innovationsleitfaden: Interagieren über Geräte

::: zone-end

::: zone target="chromeless"

# <a name="interact-through-devices"></a>Interagieren über Geräte

::: zone-end

Nehmen Sie Innovationen durch zeitweise verbundene und lernfähige Edge-Geräte vor. Orchestrieren Sie Millionen solcher Geräte, erwerben und verarbeiten Sie unbegrenzte Datenmengen, und profitieren Sie von einer wachsenden Anzahl von auf verschiedenen Geräten genutzten Funktionen, für die mehrere Sinne genutzt werden können. Für Geräte im Edge-Bereich Ihres Netzwerks bietet Azure ein Framework zum Erstellen immersiver und effektiver Geschäftslösungen. Durch universelles Computing, das durch Azure in Kombination mit KI-Technologie ermöglicht wird, können Sie jede vorstellbare Art intelligenter Anwendungen und Systeme erstellen.

Azure-Kunden verwenden eine ständig wachsende Anzahl von vernetzten Systemen und Geräten, die Daten sammeln und analysieren – nahe an Benutzern, Daten oder beidem. Benutzer erhalten Echtzeiteinblicke und -funktionen, die von schnell reagierenden und kontextbezogenen Anwendungen bereitgestellt werden. Indem Teile der Workload in den Edge-Bereich verschoben werden, benötigen diese Geräte weniger Zeit für das Senden von Nachrichten in die Cloud und können schneller auf räumliche Ereignisse reagieren.

> [!div class="checklist"]
>
> - Industrieanlagen
> - HoloLens 2
> - Azure Sphere
> - Kinect DK
> - Drohnen
> - Azure SQL-Datenbank-Edge
> - IoT Plug & Play

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-servicetabiothub"></a>[IoT-Dienst auf globaler Ebene](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Entwerfen Sie Lösungen, die eine bidirektionale Kommunikation mit IoT-Geräten im Milliardenbereich ermöglichen. Verwenden Sie integrierte Gerät-zu-Cloud-Telemetriedaten, um den Zustand Ihrer Geräte zu verstehen und Nachrichtenrouten an andere Azure-Dienste durch einfache Konfiguration zu definieren. Durch Nutzen von Nachrichten, die von der Cloud an Geräte gesendet werden, können Sie auf zuverlässige Weise Befehle und Benachrichtigungen an Ihre verbundenen Geräte senden und die Nachrichtenübermittlung mithilfe von Empfangsbestätigungen nachverfolgen. Lassen Sie das Senden von Gerätemeldungen bei Bedarf automatisch wiederholen, um zeitweilige Konnektivitätsprobleme zu überbrücken.

Dies sind einige der Features, die Sie nutzen können:

- **Noch sichererer Kommunikationskanal** zum Senden und Empfangen von Daten von IoT-Geräten
- **Integrierte Geräteverwaltung** und -bereitstellung für das bedarfsgerechte Verbinden und Verwalten von IoT-Geräten
- **Vollständige Integration mit Event Grid** und serverloses Compute zur Vereinfachung der IoT-Anwendungsentwicklung
- **Kompatibilität mit Azure IoT Edge** zum Erstellen von IoT-Hybridanwendungen

::: zone target="docs"

**Navigieren zu [IoT Hub](https://docs.microsoft.com/azure/iot-dps)**

**Navigieren zu [Device Provisioning-Dienste](https://docs.microsoft.com/azure/iot-dps)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Erstellen Sie wie folgt einen IoT-Hub:

1. Navigieren Sie zu **IoT Hub**.
2. Wählen Sie **IoT-Hub erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

<!-- markdownlint-enable DOCSMD001 -->

Der IoT Hub Device Provisioning-Dienst ist ein Hilfsdienst für IoT Hub, der eine Just-in-Time-Bereitstellung ohne manuelles Eingreifen ermöglicht.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Zum Erstellen von IoT Hub Device Provisioning-Diensten gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **IoT Hub Device Provisioning-Dienste**.
2. Wählen Sie **Device Provisioning-Dienste erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twinstabdigitaltwins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Erstellen Sie wiederverwendbare, hochgradig skalierbare und raumbezogene Umgebungen, die Streamingdaten aus der physischen und der digitalen Welt miteinander verknüpfen. Verbessern Sie Ihre Kundenbindung mit umfassenden Modellen physischer Umgebungen. Generieren Sie Raumintelligenzgraphen, um die Beziehungen und Interaktionen zwischen Personen, Bereichen und Geräten zu modellieren. Fragen Sie Daten aus einem physischen Raum ab, statt von verschiedenen Sensoren.

**Azure Digital Twins-Objektmodelle:** Eine Ontologie, in der Regionen, Orte, Etagen, Büros, Zonen, Konferenzräume und Konzentrationsräume eines intelligenten Gebäudes oder verschiedene Kraftwerke, Umspannwerke, Energieressourcen und Kunden eines Energienetzes beschrieben werden, kann mithilfe von Digital Twins-Objektmodellen und Ontologien modelliert werden.

**Raumintelligenzgraph:** Der hierarchische Graph aus Räumen, Geräten und Personen, die im Digital Twins-Objektmodell definiert sind und für den Vererbung, Filterung, Durchlaufen, Skalierbarkeit und Erweiterbarkeit unterstützt werden. Sie können Ihren Raumgraphen über eine Sammlung von in Azure gehosteten REST-APIs verwalten und nutzen.

::: zone target="docs"

**Navigieren zu [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Erstellen von Azure Digital Twins gehen Sie folgendermaßen vor:

1. Wählen Sie im linken Bereich **Ressource erstellen**.
2. Suchen Sie nach **Digital Twins**, und wählen Sie dann **Digital Twins** aus.
3. Wählen Sie **Erstellen** aus, um den Bereitstellungsprozess zu starten.
4. Zum Überprüfen vorhandener Digital Twins wählen Sie diese Schaltfläche aus:

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligencetabazuremaps"></a>[Location Intelligence](#tab/AzureMaps)

Zusätzlich zu herkömmlichen Standortfunktionen wie „In der Nähe“, „Verkehr“ und „Route“ ermöglicht es der Azure Maps-Dienst Unternehmen, Lösungen mit Location Intelligence in Echtzeit zu erstellen, die von den renommierten Partnern für Mobilitätstechnologie **TomTom** und **Moovit** gestellt wird. Integrieren Sie mit Geodiensten mühelos komplexe Standort- und Mobilitätsfunktionen in Ihre Anwendungen.

**Datendienstvorschau:** Sie können Geodaten zur Verwendung bei räumlichen Vorgängen oder bei der Bildkomposition hochladen und speichern, um die Latenz zu senken, die Produktivität zu erhöhen und neue Szenarien in Ihren Anwendungen zu ermöglichen.

**Räumliche Vorgänge:** Verbessern Sie die Location Intelligence mit einer Bibliothek aus häufig genutzten räumlichen Berechnungen, z.B. zum Geofencing, zur Ermittlung des am nächsten gelegenen Punkts und des Kreisabstands sowie für Puffer.

**Geolocation**: Finden Sie heraus, aus welchem Land/welcher Region eine IP-Adresse stammt. Passen Sie Inhalte und Dienste basierend auf Benutzerstandorten an, und erhalten Sie Einblicke in die geografische Verteilung Ihrer Kunden.

::: zone target="docs"

**Navigieren zu [Azure Maps](https://docs.microsoft.com/azure/azure-maps)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Verwenden von Location Intelligence gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Azure Maps-Konten**.
2. Wählen Sie **Azure Maps-Konten erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2Faccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiencestabspatial"></a>[Räumliche Erfahrungen](#tab/spatial)

Mit Azure Spatial Anchors können Entwickler Mixed Reality-Plattformen verwenden, um Räume wahrzunehmen, präzise Points of Interest festzulegen und diese Points of Interest von unterstützten Geräten abzurufen.

**Die echte Welt um Kontext ergänzen:** Vermitteln Sie Ihren Benutzern ein besseres Verständnis ihrer Daten – und zwar genau an dem Ort und zu dem Zeitpunkt, zu dem sie diese benötigen. Dafür müssen Sie einfach Ihre digitalen Inhalte an relevanten physischen Orten platzieren und verbinden.

**Hologramme auf verschiedenen Geräten freigeben:** Beschleunigen Sie die Entscheidungsfindung, indem Sie Ihr Team und Ihre Kunden in 3D auf den gewünschten Geräten unterstützen. Spatial Anchors erleichtert es Personen, die sich an demselben Ort befinden, an Mixed Reality-Anwendungen für mehrere Benutzer teilzunehmen.

**Ansprechende Erfahrungen:** Verbinden Sie Spatial Anchors-Instanzen miteinander, indem Sie Beziehungen zwischen diesen herstellen, und stellen Sie eine Benutzeroberfläche bereit, die zwei oder mehr Points of Interest enthält, mit denen ein Benutzer interagieren muss, um eine Aufgabe zu erfüllen. Mit Ihrer Anwendung kann ein Benutzer ein virtuelles Element in der realen Welt platzieren. In einer Industrieumgebung kann ein Benutzer beispielsweise Kontextinformationen zu einem Computer erhalten, indem er mit einer unterstützten Gerätekamera darauf zeigt.

Azure Spatial Anchors besteht aus einem verwalteten Dienst und Client-SDKs für unterstützte Geräteplattformen.

::: zone target="docs"

**Navigieren zu [Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Verwenden räumlicher Erfahrungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Spatial Anchors-Konten**.
2. Wählen Sie **Spatial Anchors-Konten erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FspatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-renderingtabremoterender"></a>[Azure Remote Rendering](#tab/RemoteRender)

Rendern Sie hochwertige interaktive 3D-Inhalte in der Cloud, und streamen Sie sie in Echtzeit auf Ihre Geräte. Renderingworkloads werden häufig für Spezialeffekte (VFX) in der Medien- und Unterhaltungsbranche eingesetzt. Rendering wird auch in vielen anderen Branchen verwendet, z.B. in der Werbebranche, im Einzelhandel, in der Öl- und Gasindustrie sowie in der Fertigungsindustrie.

Der Renderingprozess ist rechenintensiv. Es kann sein, das viele Frames oder Bilder erstellt werden müssen, und das Rendern jedes Bilds kann viele Stunden dauern. Rendering ist daher eine perfekte Workload für die Batchverarbeitung, bei der Azure und Azure Batch verwendet werden können, um viele Rendervorgänge parallel auszuführen.

::: zone target="docs"

**Navigieren zu [Azure Remote Rendering](https://azure.microsoft.com/services/remote-rendering)**

**Navigieren zu [Rendern mit Azure](https://docs.microsoft.com/azure/batch/batch-rendering-service)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Verwenden von Remote Rendering gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Batch-Konten**.
2. Wählen Sie **Batch-Konten erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FbatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
