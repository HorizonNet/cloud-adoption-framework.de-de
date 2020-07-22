---
title: Innovationstools für die Geräteinteraktion
description: Hier finden Sie Informationen zu Azure-Tools für die Interaktion über Geräte und Umgebungserfahrungen, die die natürliche Umgebung und das Verhalten von Kunden erweitern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 7ac8fe1ffb7318b3e705b4586de300cd1ee6a58f
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86449709"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Tools für die Interaktion mit Geräten in Azure

Wie im Konzeptartikel zum [Interagieren mit Geräten](../considerations/devices.md) beschrieben, hängen die Geräte für die Interaktion mit dem Kunden jeweils von den Umgebungsfunktionen ab, die zum Erfüllen der Kundenanforderung benötigt werden und die Einführung ermöglichen. Die Geschwindigkeit, mit der Ihre Lösung auf einen Auslöser der Kundenanforderung reagieren und eine diese Anforderung erfüllen kann, ist ein entscheidender Faktor für die wiederholte Verwendung. Umgebungsfunktionen verkürzen diese Reaktionszeit und verbessern das Benutzererlebnis für Ihre Kunden, indem Ihre Lösung in die unmittelbare Umgebung der Kunden integriert wird.

![Der Ansatz des Frameworks für die Cloudeinführung zum Interagieren mit Geräten](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Ausrichtung auf die Methodik

Diese Art der digitalen Erfindung kann durch eine der folgenden Ebenen der Umgebungserfahrung realisiert werden. Diese Ebenen richten sich nach der im vorhergehenden Bild dargestellten Methodik. Das Inhaltsverzeichnis auf der linken Seite enthält technische Hinweise zur Beschleunigung der digitalen Erfindung. Diese Artikel sind nach der Ebene der Umgebungserfahrung gruppiert, um sie mit der Methodik auszurichten.

- **Mobiles Erlebnis**: Mobile Apps sind häufig ein Teil der Umgebung der Kunden. In einigen Szenarien kann ein mobiles Gerät ein ausreichendes Maß an Interaktivität bieten, um eine adäquate Lösung für die Umgebung zu realisieren.
- **Mixed Reality**: Manchmal muss die natürliche Umgebung eines Kunden durch Mixed Reality verändert werden. Die Einbindung eines Kunden in diese Mixed Reality kann eine Form von Umgebungserlebnis darstellen.
- **Integrierte Realität**: Um der tatsächlichen Umgebung näher zu kommen, konzentrieren sich die Lösungen für integrierte Realität auf den Einsatz eines physischen Geräts des Kunden, um die Lösung in natürliche Verhaltensweisen einzubinden.
- **Angepasste Realität:** Wenn eine der vorherigen Umgebungslösungen prädiktive Analysen nutzt, um eine Interaktion mit einem Kunden in dessen natürlicher Umgebung bereitzustellen, sorgt diese Lösung für die höchste Form des Umgebungserlebnisses.

## <a name="toolchain"></a>Toolkette

In Azure werden häufig die folgenden Tools genutzt, um digitale Erfindungen auf allen vorherigen Ebenen von Umgebungslösungen zu beschleunigen. Diese Tools werden nach dem Grad der Erfahrung gruppiert, der erforderlich ist, um die Komplexität bei der Ausrichtung der Tools auf diese Erfahrungen zu reduzieren.

<!-- markdownlint-disable MD033 -->

| Category | Tools |
|---|---|
| Mobile Oberflächen | <li> Azure App Service <li> Power Apps <li> Power Automate <li> Intune |
| Mixed Reality | <li> Unity <li> Azure Spatial Anchors <li> HoloLens |
| Integrierte Realität | <li> Azure IoT Hub <li> Azure Sphere <li> Azure Kinect DK |
| Angepasste Realität | <li> IoT Cloud-zu-Gerät <li> Azure Digital Twins + HoloLens |

<!--markdownlint-enable MD033 -->

## <a name="get-started"></a>Erste Schritte

Im Inhaltsverzeichnis auf der linken Seite werden viele Artikel beschrieben. Diese Artikel helfen Ihnen bei den ersten Schritten mit den einzelnen Tools in dieser Toolkette.

> [!NOTE]
> Mit einigen Links verlassen Sie das Cloud Adoption Framework und erhalten weitergehende Informationen.
