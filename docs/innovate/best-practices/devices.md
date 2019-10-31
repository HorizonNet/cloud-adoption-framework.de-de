---
title: 'Cloudinnovation: Tools für die Interaktion mit Geräten in Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Tools für die Interaktion mit Geräten in Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a8dcdf770e31a1b0fb380ac0fe85bb2fe9c8ed0b
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683398"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Tools für die Interaktion mit Geräten in Azure

Wie im Theorieartikel zum [Interagieren mit Geräten](../considerations/devices.md) beschrieben, richten sich die Geräte für die Interaktion mit dem Kunden jeweils nach den Umgebungsfunktionen, die zum Erfüllen der Kundenanforderung benötigt werden und die Einführung ermöglichen. Die Geschwindigkeit, mit der Ihre Lösung auf einen Auslöser der Kundenanforderung reagieren und eine diese Anforderung erfüllen kann, ist ein entscheidender Faktor für die wiederholte Verwendung. Umgebungsfunktionen verkürzen diese Reaktionszeit und verbessern das Benutzererlebnis für Ihre Kunden, indem Ihre Lösung in die unmittelbare Umgebung der Kunden integriert wird.

![Der Ansatz des Frameworks für die Cloudeinführung zum Interagieren mit Geräten](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Ausrichten auf die Methodik

Diese Art digitaler Erfindung kann in Übereinstimmung mit der Methodik in jeder Umgebung bereitgestellt werden, wie oben dargestellt. Technische Informationen zur Beschleunigung digitaler Erfindungen finden Sie im Inhaltsverzeichnis auf der linken Seite. Diese Artikel wurden in die gleichen Umgebungen gruppiert, um sie an die Methodik anzupassen:

- **Mobiles Erlebnis**: Mobile Apps sind häufig ein Teil der Umgebung der Kunden. In einigen Szenarien kann ein mobiles Gerät ein ausreichendes Maß an Interaktivität bieten, um eine adäquate Lösung für die Umgebung zu realisieren.
- **Mixed Reality**: Manchmal muss die natürliche Umgebung eines Kunden durch Mixed Reality verändert werden. Die Einbindung von Kunden in diese Mixed Reality kann eine Form von Umgebungserlebnis darstellen.
- **Integrierte Realität**: Um der tatsächlichen Umgebung näher zu kommen, konzentrieren sich die Lösungen für integrierte Realität auf den Einsatz eines Geräts, das in der physischen Realität des Kunden existiert, um die Lösung in natürliche Verhaltensweisen einzubinden.
- **Angepasste Realität**: Wenn eine der oben genannten Umgebungslösungen prädiktive Analysen nutzt, um eine Interaktion mit dem Kunden in dessen natürlicher Umgebung bereitzustellen, sorgt diese Lösung für die höchste Form des Umgebungserlebnisses.

## <a name="toolchain"></a>Toolkette

In Azure werden häufig die folgenden Tools genutzt, um digitale Erfindungen in allen oben genannten Umgebungslösungen zu beschleunigen. Diese Tools wurden nach der Art des Benutzererlebnisses gruppiert, um die Auswahl der richtigen Tools für die verschiedenen Erlebnisse zu vereinfachen.

- Mobiles Erlebnis: App Service, PowerApps, Microsoft Flow, Intune
- Mixed Reality: Unity, Azure Spatial Anchors, HoloLens
- Integrierte Realität: Azure IoT Hub, Azure Sphere, Kinect DK
- Angepasste Realität: IoT Cloud to Device, Digital Twins + HoloLens

## <a name="get-started"></a>Erste Schritte

Das Inhaltsverzeichnis auf der linken Seite enthält viele Artikel zum Einstieg mit den einzelnen Tools in dieser Toolkette.

> [!NOTE]
> Mit einigen Links verlassen Sie das Cloud Adoption Framework und erhalten weitergehende Informationen.
