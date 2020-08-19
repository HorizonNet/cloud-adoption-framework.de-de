---
title: 'Azure-Innovation: Interagieren über Geräte'
description: Hier erfahren Sie, wie Azure mithilfe vernetzter und lernfähiger Edgegeräte ein Framework für die Erstellung immersiver und effektiver Geschäftslösungen bereitstellt.
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: aba505bea5b8bafc8a8d49a04c2a0086363d9cc4
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567868"
---
<!-- cSpell:ignore umarmohamedusman umarm Moovit -->

# <a name="interact-through-devices"></a>Interagieren über Geräte

Nehmen Sie Innovationen durch zeitweise verbundene und lernfähige Edge-Geräte vor. Orchestrieren Sie Millionen solcher Geräte, erwerben und verarbeiten Sie unbegrenzte Datenmengen, und profitieren Sie von einer wachsenden Anzahl von auf verschiedenen Geräten genutzten Funktionen, für die mehrere Sinne genutzt werden können. Für Geräte im Edge-Bereich Ihres Netzwerks bietet Azure ein Framework zum Erstellen immersiver und effektiver Geschäftslösungen. Durch universelles Computing, das durch Azure in Kombination mit KI-Technologie ermöglicht wird, können Sie jede vorstellbare Art intelligenter Anwendungen und Systeme erstellen.

Azure-Kunden verwenden eine ständig wachsende Anzahl von vernetzten Systemen und Geräten, die Daten sammeln und analysieren (nahe an Benutzern, Daten oder beidem). Benutzer erhalten Echtzeiterkenntnisse und -darstellungen, die von schnell reagierenden und kontextbezogenen Anwendungen bereitgestellt werden. Indem Teile der Workload in den Edge-Bereich verschoben werden, benötigen diese Geräte weniger Zeit für das Senden von Nachrichten in die Cloud und können schneller auf räumliche Ereignisse reagieren.

> [!div class="checklist"]
>
> - Industrieanlagen
> - [Microsoft HoloLens 2](/hololens)
> - [Azure Sphere](/azure-sphere/product-overview/what-is-azure-sphere)
> - [Azure Kinect DK](/azure/kinect-dk/about-azure-kinect-dk)
> - Drohnen
> - [Azure SQL Edge](/azure/azure-sql-edge/overview)
> - [IoT Plug & Play](/azure/iot-pnp/overview-iot-plug-and-play)

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-service"></a>[IoT-Dienst auf globaler Ebene](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Entwerfen Sie Lösungen, die eine bidirektionale Kommunikation mit IoT-Geräten im Milliardenbereich ermöglichen. Verwenden Sie integrierte Gerät-zu-Cloud-Telemetriedaten, um den Zustand Ihrer Geräte zu verstehen und Nachrichtenrouten an andere Azure-Dienste durch einfache Konfiguration zu definieren. Durch Nutzen von Nachrichten, die von der Cloud an Geräte gesendet werden, können Sie auf zuverlässige Weise Befehle und Benachrichtigungen an Ihre verbundenen Geräte senden und die Nachrichtenübermittlung mithilfe von Empfangsbestätigungen nachverfolgen. Lassen Sie das Senden von Gerätemeldungen bei Bedarf automatisch wiederholen, um zeitweilige Konnektivitätsprobleme zu überbrücken.

Dies sind einige der Features, die Sie nutzen können:

- **Noch sichererer Kommunikationskanal** zum Senden und Empfangen von Daten von IoT-Geräten
- **Integrierte Geräteverwaltung** und -bereitstellung für das bedarfsgerechte Verbinden und Verwalten von IoT-Geräten
- **Vollständige Integration mit Event Grid** und serverloses Compute zur Vereinfachung der IoT-Anwendungsentwicklung
- **Kompatibilität mit Azure IoT Edge** zum Erstellen von IoT-Hybridanwendungen

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure IoT Hub](/azure/iot-hub)
- [Azure IoT Hub Device Provisioning Service (DPS)](/azure/iot-dps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Erstellen Sie wie folgt einen IoT-Hub:

1. Navigieren Sie zu **IoT Hub**.
2. Wählen Sie **IoT-Hub erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

<!-- markdownlint-enable DOCSMD001 -->

Azure IoT Hub Device Provisioning Service ist ein Hilfsdienst für IoT Hub, der eine Just-in-Time-Bereitstellung ohne manuelles Eingreifen ermöglicht.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

So erstellen Sie einen Azure IoT Hub Device Provisioning Service:

1. Navigieren Sie zu **Device Provisioning Services**.
2. Wählen Sie **Hinzufügen**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Erstellen Sie wiederverwendbare, hochgradig skalierbare und raumbezogene Umgebungen, die Streamingdaten aus der physischen und der digitalen Welt miteinander verknüpfen. Verbessern Sie Ihre Kundenbindung mit umfassenden Modellen physischer Umgebungen. Generieren Sie Raumintelligenzgraphen, um die Beziehungen und Interaktionen zwischen Personen, Bereichen und Geräten zu modellieren. Fragen Sie Daten aus einem physischen Raum ab, statt von verschiedenen Sensoren.

**Azure Digital Twins-Objektmodelle:** Eine Ontologie, in der Regionen, Orte, Etagen, Büros, Zonen, Konferenzräume und Konzentrationsräume eines intelligenten Gebäudes oder verschiedene Kraftwerke, Umspannwerke, Energieressourcen und Kunden eines Energienetzes beschrieben werden, kann mithilfe von Digital Twins-Objektmodellen und Ontologien modelliert werden.

**Raumintelligenzgraph:** Der hierarchische Graph aus Räumen, Geräten und Personen, die im Digital Twins-Objektmodell definiert sind und für den Vererbung, Filterung, Durchlaufen, Skalierbarkeit und Erweiterbarkeit unterstützt werden. Sie können Ihren Raumgraphen über eine Sammlung von in Azure gehosteten REST-APIs verwalten und nutzen.

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Digital Twins](/azure/digital-twins/about-digital-twins)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Erstellen von Azure Digital Twins gehen Sie folgendermaßen vor:

1. Wählen Sie im linken Bereich **Ressource erstellen**.
2. Suchen Sie nach **Digital Twins**, und wählen Sie dann **Digital Twins** aus.
3. Wählen Sie **Erstellen** aus, um den Bereitstellungsprozess zu starten.
4. Wählen Sie zum Überprüfen vorhandener Digital Twins diese Schaltfläche aus:

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligence"></a>[Location Intelligence](#tab/AzureMaps)

Zusätzlich zu herkömmlichen Standortfunktionen wie „In der Nähe“, „Verkehr“ und „Route“ ermöglicht es der Azure Maps-Dienst Unternehmen, Lösungen mit Location Intelligence in Echtzeit zu erstellen, die von den renommierten Partnern für Mobilitätstechnologie TomTom und Moovit gestellt wird. Integrieren Sie mit Geodiensten mühelos komplexe Standort- und Mobilitätsfunktionen in Ihre Anwendungen.

**Azure Maps-Datendienst (Vorschauversion):** Sie können Geodaten zur Verwendung bei räumlichen Vorgängen oder bei der Bildkomposition hochladen und speichern, um die Latenz zu senken, die Produktivität zu erhöhen und neue Szenarien in Ihren Anwendungen zu ermöglichen.

**Räumliche Vorgänge:** Verbessern Sie die Location Intelligence mit einer Bibliothek aus häufig genutzten räumlichen Berechnungen, z.B. zum Geofencing, zur Ermittlung des am nächsten gelegenen Punkts und des Kreisabstands sowie für Puffer.

**Geolocation**: Finden Sie heraus, aus welchem Land/welcher Region eine IP-Adresse stammt. Passen Sie Inhalte und Dienste basierend auf Benutzerstandorten an, und erhalten Sie Einblicke in die geografische Verteilung Ihrer Kunden.

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Maps](/azure/azure-maps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

So verwenden Sie Location Intelligence

1. Navigieren Sie zu **Azure Maps-Konten**.
2. Wählen Sie **Azure Maps-Konten erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2FAccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiences"></a>[Räumliche Erfahrungen](#tab/spatial)

Mit Azure Spatial Anchors können Entwickler Mixed Reality-Plattformen verwenden, um Räume wahrzunehmen, präzise Points of Interest festzulegen und diese Points of Interest von unterstützten Geräten abzurufen.

**Die echte Welt um Kontext ergänzen:** Vermitteln Sie Ihren Benutzern ein besseres Verständnis ihrer Daten – und zwar genau an dem Ort und zu dem Zeitpunkt, zu dem sie diese benötigen. Dafür müssen Sie einfach Ihre digitalen Inhalte an relevanten physischen Orten platzieren und verbinden.

**Hologramme auf verschiedenen Geräten freigeben:** Beschleunigen Sie die Entscheidungsfindung, indem Sie Ihr Team und Ihre Kunden in 3D auf den gewünschten Geräten unterstützen. Raumanker vereinfachen es für Personen, die sich am selben Ort befinden, an Mixed Reality-Anwendungen für mehrere Benutzer teilzunehmen.

**Ansprechende Erfahrungen:** Verbinden Sie Spatial Anchors-Instanzen miteinander, indem Sie Beziehungen zwischen diesen herstellen, und stellen Sie eine Benutzeroberfläche bereit, die zwei oder mehr Points of Interest enthält, mit denen ein Benutzer interagieren muss, um eine Aufgabe zu erfüllen. Mit Ihrer Anwendung kann ein Benutzer ein virtuelles Artefakt in der realen Welt platzieren. In einer Industrieumgebung kann ein Benutzer beispielsweise Kontextinformationen zu einem Computer erhalten, indem er mit einer unterstützten Gerätekamera darauf zeigt.

Azure Spatial Anchors besteht aus einem verwalteten Dienst und Client-SDKs für unterstützte Geräteplattformen.

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Spatial Anchors](/azure/spatial-anchors/overview)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

So verwenden Sie Azure Spatial Anchors

1. Navigieren Sie zu **Spatial Anchors accounts** (Spatial Anchors-Konten).
2. Wählen Sie **Create Spatial Anchors account** (Spatial Anchors-Konto erstellen) aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FSpatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-rendering"></a>[Azure Remote Rendering](#tab/RemoteRender)

Rendern Sie hochwertige interaktive 3D-Inhalte in der Cloud, und streamen Sie sie in Echtzeit auf Ihre Geräte. Renderingworkloads werden häufig für Spezialeffekte (VFX) in der Medien- und Unterhaltungsbranche eingesetzt. Rendering wird auch in vielen anderen Branchen verwendet, z.B. in der Werbebranche, im Einzelhandel, in der Öl- und Gasindustrie sowie in der Fertigungsindustrie.

Der Renderingprozess ist rechenintensiv. Es kann sein, das viele Frames oder Bilder erstellt werden müssen, und das Rendern jedes Bilds kann viele Stunden dauern. Rendering ist daher eine perfekte Workload für die Batchverarbeitung, bei der Azure und Azure Batch verwendet werden können, um viele Rendervorgänge parallel auszuführen.

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Remote Rendering](/azure/remote-rendering/overview/about)
- [Rendern mit Azure](/azure/batch/batch-rendering-service)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Zum Verwenden von Remote Rendering gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Batch-Konten**.
2. Wählen Sie **Batch-Konten erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FBatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
