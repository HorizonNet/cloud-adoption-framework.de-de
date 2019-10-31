---
title: 'Azure-Innovationsleitfaden: Demokratisieren von Daten'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie Daten mithilfe von Azure demokratisieren.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 65c1ecd1d722286fb495af3069862131629c35d1
ms.sourcegitcommit: 0d14d89b9004a65a322724342cb5086ad2c77467
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777087"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Azure-Innovationsleitfaden: Demokratisieren von Daten

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratisieren von Daten

::: zone-end

Einer der ersten Schritte zum Demokratisieren von Daten ist das Verbessern ihrer Auffindbarkeit. Durch Katalogisieren und Verwalten der Datenfreigabe können Unternehmen den größten Nutzen aus den vorhandenen Informationsressourcen ziehen. Ein Datenkatalog macht Datenquellen für Benutzer, die die Daten verwalten, einfach ermittelbar und verständlich. Azure Data Catalog ermöglicht die Verwaltung innerhalb eines Unternehmens, während Azure Data Share die Verwaltung und Freigabe außerhalb des Unternehmens ermöglicht.

Azure-Dienste, die eine Verarbeitung der Daten bieten (z.B. Azure Time Series Insights und Stream Analytics), sind weitere Funktionen, die von Kunden und Partnern erfolgreich für Ihre Innovationsanforderungen genutzt werden.

# <a name="catalogtabcatalog"></a>[Katalog](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Azure Data Catalog setzt bei den Ermittlungsanforderungen der Datenconsumer an und ermöglicht Datenproduzenten die Verwaltung von Informationsressourcen. Überwinden Sie die Kluft zwischen IT- und Geschäftsbereichen, sodass alle Beteiligten ihre Kenntnisse einbringen können. Speichern Sie Ihre Daten, wo Sie möchten, und setzen Sie die Tools Ihrer Wahl ein. Steuern Sie, wer auf Ihre registrierten Datenbestände zugreifen kann. Integrieren Sie vorhandene Tools und bestehende Verfahren mit offenen REST-APIs.

> [!div class="checklist"]
>
> - Registrieren
> - Suchen und Kommentieren
> - Verbinden und Verwalten

::: zone target="docs"

**Navigieren zu [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

Es wird pro Organisation nur ein Azure Data Catalog unterstützt. Wenn bereits ein Katalog für Ihre Organisation erstellt wurde, können Sie keine zusätzlichen Kataloge hinzufügen.

Zum Erstellen von Azure Data Catalog für Ihre Organisation gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Azure Data Catalog**.
2. Klicken Sie auf die Schaltfläche **Erstellen** .

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Freigabe](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Ein ausgewogenes Gleichgewicht zwischen offener Freigabe von Daten und der Kontrolle darüber, für wen und welche Daten freigegeben werden, ist ein maßgeblicher Faktor für Innovation. Bei den Bemühungen zum Demokratisieren von Daten können Organisation leicht durch den enormen Umfang, die Geschwindigkeit und den Lebenszyklus dieser Daten überfordert sein. Mit Azure Data Share ist sichergestellt, dass der Datenanbieter steuern kann, wie seine Daten verarbeitet werden, indem er Nutzungsbedingungen für die Datenfreigabe angibt. Der Datenconsumer muss diese Bedingungen akzeptieren, bevor er Daten empfangen kann. Datenanbieter können die Häufigkeit angeben, mit der Datenconsumer Updates erhalten. Der Zugriff auf neue Updates kann vom Datenanbieter jederzeit widerrufen werden.

> [!div class="checklist"]
>
> - Erstellen einer Datenfreigabe
> - Hinzufügen von Datasets zu Ihrer Datenfreigabe
> - Aktivieren eines Synchronisierungszeitplans für Ihre Datenfreigabe
> - Hinzufügen von Empfängern zu Ihrer Datenfreigabe

::: zone target="docs"
**Navigieren zu [Azure Data Share](https://docs.microsoft.com/azure/data-share)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Zum Erstellen einer Datenfreigabe gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Azure Data Share**.
2. Klicken Sie auf **Datenfreigabe erstellen**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Share" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Verwenden Sie [öffentliche Azure-Datasets](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets), um Ihre Analyse durch Einbeziehung von Daten zu [Feiertagen](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays), [Wetter](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system) und [räumliche Bilder](https://azure.microsoft.com/services/open-datasets/catalog/hls) in Ihre Modelle zu verbessern.

Die hier angegebenen Informationen zum [Demokratisieren von Geschäftsprozessen](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) und zur [Unterstützung von entwickelnden Anwendern](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers) werden in den nächsten Schritten behandelt.

# <a name="insightstabinsights"></a>[Erkenntnisse](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Durchsuchen von Datenströmen nahezu in Echtzeit, Speicherung auf mehreren Ebenen für IoT-Zeitreihendaten, Modelle zur Kontextualisierung der Telemetrierohdaten, Ableitung von objektbasierten Erkenntnissen – die Möglichkeiten der Dateninnovation sind endlos. Sie können eine reibungslose und kontinuierliche Integration mit anderen Datenlösungen sowie Ursachenanalysen und Anomalieerkennung bereitstellen, einschließlich benutzerdefinierter Anwendungsoptionen auf der Time Series Insights-Plattform.

> [!div class="checklist"]
>
> - Planen Ihrer Time Series Insights-Umgebung
> - Visualisieren von Daten im Explorer
> - Grundlegendes zur Datenaufbewahrung
> - Entwickeln und Freigeben von benutzerdefinierten Ansichten

::: zone target="docs"

**Navigieren zu [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Aktion

Zum Erstellen einer Azure Time Series Insights-Umgebung gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Azure Time Series Insights**.
2. Klicken Sie auf **Time Series Insights-Umgebung erstellen**.
3. Verweisen Sie diese Umgebung auf eine Ereignisquelle, entweder IOT Hub oder Event Hub.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
