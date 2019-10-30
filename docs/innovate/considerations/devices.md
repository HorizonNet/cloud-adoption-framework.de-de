---
title: 'Cloudinnovation: Interagieren mit Geräten'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in Cloudinnovation: Interagieren mit Geräten'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5a9ec9f38d89683482d7f98923aa0ef2ccf201b9
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683215"
---
# <a name="ambient-experiences-interact-with-devices"></a>Umgebungserfahrungen: Interagieren mit Geräten

Unter [Entwickeln von Lösungen mit Blick auf die Kundenanforderungen](./build.md) haben wir die drei Tests wahrer Innovation erörtert: Erfüllung eines Kundenbedürfnisse, dauerhafte Bindung des Kunden, Skalierung in einem Stamm von Kundenkohorten. Jeder Test Ihrer Hypothese erfordert Aufwand und Iterationen hinsichtlich des Ansatzes zur Umsetzung. Dieser Artikel bietet Einblicke in einige weitergehende Ansätze, um diesen Aufwand mittels **Umgebungserfahrungen** zu verringern. Durch die Interaktion mit Geräten statt mit einer Anwendung kann es sein, dass sich der Kunde eher zuerst Ihrer Lösung zuwendet, um seine Bedürfnisse zu erfüllen.

## <a name="ambient-experiences"></a>Umgebungserfahrungen

Eine Umgebungserfahrung ist eine digitale Erfahrung in Bezug auf die unmittelbare Umgebung. Eine Lösung mit Umgebungserfahrungen ist darauf ausgerichtet, den Kunden im Moment seines Bedürfnisses zu erreichen. Wenn möglich, erfüllt die Lösung das Kundenbedürfnis, ohne den natürlichen Ablauf seiner gegenwärtigen Aktivität zu verlassen.

Das Leben in der digitalen Wirtschaft ist voller Ablenkungen. Wir alle werden mit Nachrichten, ob visuell oder verbal, aus sozialen Medien, per E-Mail oder dem Internet, bombardiert, von denen jede ein Ablenkungsrisiko darstellt. Das Ablenkungsrisiko steigt mit jeder Sekunde zwischen dem Moment des Bedürfnisses des Kunden und einer Interaktion mit der Lösung. Unzählige Kunden gehen in dieser kurzen Zeitspanne verloren. Um einen Anstieg wiederholter Akzeptanz zu fördern, verringern Sie die Anzahl der Ablenkungen, indem Sie die Zeit bis zur Lösung verkürzen.

## <a name="interacting-with-devices"></a>Interagieren mit Geräten

Eine standardmäßige Weboberfläche ist die verbreitetste Anwendungsentwicklungstechnik zur Erfüllung von Kundenbedürfnissen. Die Annahme bei diesem Ansatz ist, dass sich der Kunde an seinem Computer befindet. Wenn Ihr Kunde seine Bedürfnisse stets am Laptop erfüllt, entwickeln Sie eine Web-App. Diese Web-App bietet dem Kunden in diesem Szenario eine „Umgebungserfahrung“. Aber wir wissen, dass dieses Szenario in der modernen Gesellschaft immer weniger wahrscheinlich sein wird.

![Umgebungserfahrungen](../../_images/innovate/ambient-experiences.png)

Umgebungserfahrungen, wie oben dargestellt, erfordern in der Regel mehr als eine Web-App. Durch [Messungen](./measure.md) und [Lernen vom Kunden](./learn.md) kann das Verhalten, das zum Bedürfnisauslöser des Kunden führt, beobachtet, verfolgt und genutzt werden, um eine bessere Umgebungserfahrung zu schaffen. Im Folgenden werden einige Ansätze zur Einbeziehung von Umgebungslösungen in Ihre Hypothesen zusammengefasst. Weitere Details dazu finden Sie in den folgenden Abschnitten.

- **[Mobile Erfahrung](#mobile-experience)** : Ähnlich wie ein Laptop sind mobile Apps häufig ein Teil der Umgebung der Kunden. In einigen Szenarien kann dies ein ausreichendes Maß an Interaktivität bieten, um eine adäquate Lösung für die Umgebung zu realisieren.
- **[Mixed Reality](#mixed-reality):** Mitunter muss die natürliche Umgebung eines Kunden verändert werden, um eine entsprechende Interaktion zu ermöglichen. Dadurch wird eine Art falsche Realität geschaffen, in der der Kunde mit der Lösung interagieren und ein Bedürfnis erfüllen kann. In diesem Fall ist die Lösung innerhalb der falschen Realität umgebungsgerecht.
- **[Integrierte Realität](#integrated-reality):** Um der tatsächlichen Umgebung näher zu kommen, konzentrieren sich Lösungen für integrierte Realität auf den Einsatz eines Geräts, das in der Realität des Kunden existiert, um die Lösung in natürliche Verhaltensweisen einzubinden. Ein virtueller Assistent ist ein gutes Beispiel für die Integration von Realität in die Umgebung. Eine weniger bekannte Option ist die Nutzung von IoT-Technologien (Internet of Things, Internet der Dinge) zur Einbindung von Geräten, die bereits in der Umgebung des Kunden vorhanden sind.
- **[Angepasste Realität](#adjusted-reality):** Wenn für eine der oben genannten Umgebungslösungen eine prädiktive Analyse in der Cloud genutzt wird, um eine Interaktion mit dem Kunden in der natürlichen Umgebung zu definieren und bereitzustellen, zeichnet sich die Lösung durch eine angepasste Realität aus.

Das Erfassen der Kundenbedürfnisse und das Messen der Auswirkung auf den Kunden hilft bei der Entscheidung, ob eine Interaktion mit einem Gerät oder eine Umgebungserfahrung erforderlich ist, um Ihre Hypothese zu bestätigen. Mithilfe jedes dieser Datenpunkte werden die folgenden Abschnitte Ihnen helfen, die beste Lösung zu finden.

## <a name="mobile-experience"></a>Mobile Erfahrung

Die erste Phase der Umgebungserfahrung ist, sich vom Computer zu lösen. Die heutigen Verbraucher und Geschäftsleute bewegen sich fließend zwischen mobilen Geräten und PCs. Alle von Ihrem Kunden genutzten Plattformen oder Geräte schaffen für den Kunden potenziell eine neue Erfahrung. Das Hinzufügen einer mobilen Erfahrung zur Erweiterung der primären Lösung ist der schnellste Weg, um die Einbindung in die unmittelbare Umgebung des Kunden zu verbessern. Wenngleich ein mobiles Gerät weit von einer Umgebungserfahrung entfernt ist, könnte es näher an den Moment des Bedürfnisses des Kunden heranrücken.

Wenn Kunden mobil sind und häufig ihren Standort wechseln, kann dies die relevanteste Form der Umgebungserfahrung für eine bestimmte Lösung sein. Eine gängige Innovationsquelle in den letzten zehn Jahren war die Erweiterung bestehender Lösungen durch Integration einer mobilen Erfahrung.

Beispiele für diesen Ansatz finden Sie in Azure App Services. Während der ersten Iterationen kann die [Web-App-Funktion von Azure App Service](/azure/app-service/overview) zum Testen der Hypothese verwendet werden. Mit zunehmender Komplexität der Hypothesen kann die [mobile App-Funktion von Azure App Services](/azure/app-service-mobile/) die Web-App so erweitern, dass sie auf einer Vielzahl mobiler Plattformen ausgeführt wird.

## <a name="mixed-reality"></a>Mixed Reality

Der nächste Reifegrad bei Umgebungserfahrungen ist die Erweiterung oder Replikation der Kundenumgebung durch Mixed-Reality-Lösungen. Bei diesem Ansatz wird die Lösung umgebungsrelevanter, indem sie für den Kunden eine Erweiterung der Realität erzeugt, in der er agieren kann.

> [!IMPORTANT]
> Wenn ein VR-Gerät (Virtual Reality) benötigt wird und *nicht bereits Teil der unmittelbaren Umgebung oder des natürlichen Verhaltens* ist, dann ist Augmented/Virtual Reality eher eine alternative Erfahrung als eine Umgebungserfahrung.

Diese Art von Erfahrung ist zunehmend für remote tätige Arbeitskräfte üblich. Der Einsatz dieser Erfahrungen steigt noch schneller in Branchen, die eine Kooperation oder Fachkompetenz benötigen, die auf dem lokalen Markt nicht ohne Weiteres verfügbar ist. Ein typisches Szenario, bei dem Augmented Reality als Teil eines natürlichen Verhaltens erforderlich ist, ist die zentralisierte Implementierungsunterstützung eines komplexen Produkts für remote tätige Arbeitskräfte. In diesen Szenarien können das zentrale Supportteam und der remote tätige Mitarbeiter Augmented Reality einsetzen, um Fehler zu beheben oder das Produkt zu installieren.

Im obigen oder ähnlichen Szenarien wäre ein Beispiel einer Umgebungserfahrung die Verwendung von Raumankern. Raumanker ermöglichen Ihnen das Erzeugen von Mixed Reality-Umgebungen mit Objekten, die ihre Position im Zeitverlauf geräteübergreifend beibehalten. Durch Raumanker kann ein bestimmtes Verhalten erfasst, aufgezeichnet und beibehalten werden, das eine Umgebungserfahrung bietet, wenn der Benutzer das nächste Mal innerhalb dieser erweiterten Umgebung arbeitet. [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview) ist ein Dienst, der diese Logik in die Cloud verlagert und es ermöglicht, Erfahrungen zwischen Geräten und sogar zwischen Lösungen zu teilen.

## <a name="integrated-reality"></a>Integrierte Realität

Jenseits mobiler Realität oder gar Mixed Reality liegt der Einsatz integrierter Realität. Bei diesem Ansatz geht es darum, die digitale Erfahrung vollständig abzuschaffen. Überall um uns herum befinden sich Geräte mit Compute- und Verbindungsfunktionen. Mit diesen Geräten können Daten aus der unmittelbaren Umgebung erfasst werden, ohne dass der Kunde dafür ein Smartphone, einen Laptop oder ein VR-Gerät bedienen muss.

Diese Form der Erfahrung ist ideal, wenn sich eine bestimmte Art von Gerät stets in der gleichen Umgebung befindet, in der die Kundenbedürfnisse entstehen. Übliche Szenarien sind Fabrikhallen, Aufzüge oder sogar Ihr Auto. Diese Art großformatiger Geräte verfügt bereits über Computeleistung. Sie können auch Daten vom Gerät selbst verwenden, um Kundenverhalten zu erkennen und diese Verhaltensweisen in die Cloud zu übertragen. Diese automatische Erfassung von Daten zum Kundenverhalten reduziert die Notwendigkeit der Dateneingabe durch einen Kunden erheblich. Darüber hinaus kann die Web-, mobile oder VR-Erfahrung als Feedbackschleife genutzt werden, um auszutauschen, was die Lösung für integrierte Realität gelernt hat.

Beispiele für integrierte Realität in Azure sind u. a.:

- [Azure IoT-Lösungen](https://docs.microsoft.com/azure/iot-fundamentals), eine Sammlung von Diensten in Azure, die alle bei der Verwaltung von Geräten und dem Fluss von Daten von diesen Geräten in die Cloud und zurück zu Endbenutzern helfen.
- [Azure Sphere](/azure-sphere) ist eine Kombination aus Hardware und Software und eine standardmäßig sichere Möglichkeit, einem bestehenden Gerät zu ermöglichen, Daten zwischen sich und Azure IoT-Lösungen sicher zu übertragen.
- Das [Azure Kinect Developers Kit](https://docs.microsoft.com/azure/Kinect-dk) bietet mit fortschrittlichen Modellen für maschinelles Sehen und Sprachmodellen KI-Sensoren, die Bild- und Audiodaten in der unmittelbaren Umgebung sammeln und diese in Ihre Lösung einbringen können.

Alle drei Lösungen ermöglichen die Erfassung von Daten in der natürlichen Umgebung zum Zeitpunkt des Kundenbedürfnisses. Anschließend kann Ihre Lösung auf diese Dateneingaben reagieren, um das Bedürfnis zu erfüllen, manchmal bevor der Kunde überhaupt weiß, dass ein Auslöser für dieses Bedürfnis entstanden ist.

## <a name="adjusted-reality"></a>Angepasste Realität

Die höchste Form der Umgebungserfahrung ist die angepasste Realität, die oft als Umgebungsintelligenz bezeichnet wird. Angepasste Realität ist ein Ansatz zur Nutzung von Informationen aus Ihrer Lösung, um die Realität des Kunden zu beeinflussen, ohne dass eine direkte Interaktion mit einer Anwendung erforderlich ist. Bei diesem Ansatz ist die Anwendung, die Sie ursprünglich zum Nachweis Ihrer Hypothese entwickelt haben, möglicherweise völlig unwichtig. Stattdessen erleichtern die Geräte in der Umgebung die Ein- und Ausgaben, um die Bedürfnisse der Kunden zu decken.

Virtuelle Assistenten und intelligente Lautsprecher sind ein gutes Beispiel für angepasste Realität. Allein ist ein intelligenter Lautsprecher ein Beispiel für einfache integrierte Realität. Fügen Sie einer intelligenten Lautsprecherlösung einen intelligenten Licht- und Bewegungssensor hinzu, und es ist ganz einfach, eine einfache Lösung zu schaffen, bei der das Licht beim Betreten eines Raums eingeschaltet wird.

Fabrikhallen auf der ganzen Welt bieten zusätzliche Szenarien angepasster Realität. In frühen Phasen integrierter Realität erkannten Sensoren an Geräten Bedingungen wie Überhitzung und meldeten einem Bediener über eine Anwendung die Notwendigkeit eines Eingriffs. Bei angepasster Realität kann der Kunde noch immer involviert sein. Aber die Feedbackschleife ist straffer. In einer Fabrikhalle mit angepasster Realität erkennt ein Gerät eine Überhitzung in einer kritischen Maschine irgendwo an der Montagelinie. An anderer Stelle in der Halle verlangsamt dann ein zweites Gerät die Produktion etwas, damit die Maschine abkühlen und das Tempo wieder aufnehmen kann, nachdem der Vorfall behoben wurde. In diesem Szenario spielt der Kunde keine wesentliche Rolle mehr. Der Kunde verwendet Ihre Anwendung, um die Regeln festzulegen und zu verstehen, wie sich diese Regeln auf die Produktion ausgewirkt haben, ist jedoch kein erforderlicher Teil der Feedbackschleife.

Die Azure-Dienste im vorherigen Abschnitt, [Azure IoT-Lösungen](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](/azure-sphere) und [Azure Kinect Developers Kit](https://docs.microsoft.com/azure/Kinect-dk) könnten jeweils Komponenten einer Lösung für angepasste Realität sein. Ihre ursprüngliche Anwendungs- und Geschäftslogik dient dabei als Vermittler zwischen den Eingaben aus der Umgebung und den Änderungen, die an der physischen Umgebung vorgenommen werden müssen.

Ein weiteres Beispiel angepasster Realität ist die Herstellung eines digitalen Zwillings, bei dem es sich um eine digitale Darstellung eines physischen Geräts in einem Computer-, mobilen oder Mixed-Reality-Format handelt. Im Gegensatz zu weniger komplexen 3D-Modellen spiegelt ein digitaler Zwilling Daten wider, die von einem realen Gerät in der physischen Umgebung gesammelt wurden. Dies ermöglicht dem Benutzer, mit der digitalen Darstellung auf eine Weise zu interagieren, die in der realen Welt unmöglich wäre. Bei diesem Ansatz passen die physischen Geräte eine Mixed-Reality-Umgebung an. Aber die Lösung sammelt nach wie vor Daten aus einer Lösung mit integrierter Realität und nutzt diese, um die Realität der aktuellen Umgebung des Kunden zu gestalten.

In Azure dient ein Dienst namens [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins) zum Erstellen von und Zugreifen auf digitale Zwillinge.

## <a name="next-steps"></a>Nächste Schritte

Mit einem fundierten Verständnis der Interaktionen von Geräten und Umgebungserfahrung, die für Ihre Lösung geeignet ist, sind Sie nun bereit, die abschließende Fachrichtung im Bereich Innovation zu erkunden, [Vorhersagen und Beeinflussen](./predict.md).

> [!div class="nextstepaction"]
> [Vorhersagen und Beeinflussen](./predict.md)
