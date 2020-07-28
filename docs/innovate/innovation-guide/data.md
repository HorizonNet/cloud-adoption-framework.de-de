---
title: 'Azure-Innovation: Demokratisieren von Daten'
description: Hier finden Sie Informationen zu Azure Data Catalog, Azure Data Share und anderen Tools, die die Auffindbarkeit und das Verständnis von Daten verbessern.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0ac9256adda2b310592d69685a183b790790228a
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86449012"
---
# <a name="democratize-data"></a>Demokratisieren von Daten

Einer der ersten Schritte zum Demokratisieren von Daten ist das Verbessern ihrer Auffindbarkeit. Durch Katalogisieren und Verwalten der Datenfreigabe können Unternehmen den größten Nutzen aus den vorhandenen Informationsressourcen ziehen. Ein Datenkatalog sorgt dafür, dass Datenquellen von den Benutzern, die die Daten verwalten, leicht ermittelt und verstanden werden können. Azure Data Catalog ermöglicht die Verwaltung innerhalb eines Unternehmens, während Azure Data Share die Verwaltung und Freigabe außerhalb des Unternehmens ermöglicht.

Azure-Dienste, die eine Verarbeitung der Daten bieten (z.B. Azure Time Series Insights und Stream Analytics), sind weitere Funktionen, die von Kunden und Partnern erfolgreich für Ihre Innovationsanforderungen genutzt werden.

## <a name="catalog"></a>[Katalog](#tab/Catalog)

### <a name="azure-data-catalog"></a>Azure Data Catalog

Azure Data Catalog setzt bei den Ermittlungsanforderungen der Datenconsumer an und ermöglicht Datenproduzenten die Verwaltung von Informationsressourcen. Data Catalog überwindet die Kluft zwischen IT- und Geschäftsbereichen, sodass alle Beteiligten ihre Kenntnisse einbringen können. Sie können Ihre Daten an der gewünschten Stelle speichern und mit den Tools, die Sie verwenden möchten, eine Verbindung mit ihnen herstellen. Mit Azure Data Catalog können Sie steuern, wer registrierte Datenressourcen ermitteln kann. Sie können vorhandene Tools und bestehende Verfahren mit offenen REST-APIs integrieren.

> [!div class="checklist"]
>
> - Register
> - Suchen und Kommentieren
> - Verbinden und Verwalten

::: zone target="docs"

**Zur [Azure Data Catalog-Dokumentation](https://docs.microsoft.com/azure/data-catalog) navigieren**

::: zone-end

::: zone target="chromeless"

#### <a name="action"></a>Aktion

Pro Organisation kann immer nur eine einzelne Azure Data Catalog-Instanz verwendet werden. Wenn für Ihr Unternehmen bereits ein Katalog erstellt wurde, können keine weiteren Kataloge hinzugefügt werden.

So erstellen Sie einen Katalog für Ihre Organisation:

1. Navigieren Sie zu **Azure Data Catalog**.
2. Klicken Sie auf **Erstellen**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2FCatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="share"></a>[Teilen](#tab/Share)

### <a name="azure-data-share"></a>Azure Data Share

Ein ausgewogenes Gleichgewicht zwischen offener Freigabe von Daten und der Kontrolle darüber, für wen und welche Daten freigegeben werden, ist ein maßgeblicher Faktor für Innovation. Bei den Bemühungen zum Demokratisieren von Daten können Organisation leicht durch den enormen Umfang, die Geschwindigkeit und den Lebenszyklus dieser Daten überfordert sein. Azure Data Share stellt sicher, dass Datenanbieter steuern können, wie ihre Daten verarbeitet werden, indem sie Nutzungsbedingungen für die Datenfreigabe angeben. Der Datenconsumer muss diese Bedingungen vor dem Empfang der Daten akzeptieren. Datenanbieter können die Häufigkeit angeben, mit der Datenconsumer Updates erhalten. Der Zugriff auf neue Updates kann vom Datenanbieter jederzeit widerrufen werden.

> [!div class="checklist"]
>
> - Erstellen Sie eine Datenfreigabe.
> - Fügen Sie Ihrer Datenfreigabe Datasets hinzu.
> - Aktivieren Sie einen Synchronisierungszeitplan für Ihre Datenfreigabe.
> - Fügen Sie Ihrer Datenfreigabe Empfänger hinzu.

::: zone target="docs"

**Zur [Azure Data Share-Dokumentation](https://docs.microsoft.com/azure/data-share) navigieren**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

#### <a name="action"></a>Aktion

So erstellen Sie eine Datenfreigabe:

1. Navigieren Sie zu **Azure Data Share**.
2. Wählen Sie **Datenfreigabe erstellen** aus.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2FAccounts]" submitText="Go to Azure Data Shares" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="insights"></a>[Erkenntnisse](#tab/Insights)

### <a name="azure-time-series-insights"></a>Azure Time Series Insights

Die Dateninnovationsmöglichkeiten von Azure Time Series Insights sind endlos. Die Anwendung bietet Untersuchung von Datenströmen nahezu in Echtzeit und mehrschichtigen Speicher für Zeitreihendaten mit IoT-Skalierung. Sie bietet außerdem Modelle zum Kontextualisieren von Telemetrierohdaten und Gewinnen von ressourcenbasierten Erkenntnissen. Sie können eine reibungslose und kontinuierliche Integration mit anderen Datenlösungen sowie Ursachenanalysen und Anomalieerkennung bereitstellen, einschließlich benutzerdefinierter Anwendungsoptionen auf der Time Series Insights-Plattform.

> [!div class="checklist"]
>
> - Planen Ihrer Time Series Insights-Umgebung
> - Visualisieren von Daten im Explorer
> - Grundlegendes zur Datenaufbewahrung
> - Entwickeln und Freigeben von benutzerdefinierten Ansichten

::: zone target="docs"

**Zu [Übersicht über Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview) navigieren**

::: zone-end

::: zone target="chromeless"

#### <a name="action"></a>Aktion

Zum Erstellen einer Azure Time Series Insights-Umgebung gehen Sie folgendermaßen vor:

1. Zu **Azure Time Series Insights-Umgebungen** navigieren.
2. Wählen Sie **Time Series Insights-Umgebung erstellen** aus.
3. Verweisen Sie diese Umgebung auf eine Ereignisquelle, entweder Azure IoT Hub oder Event Hubs.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2FEnvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
