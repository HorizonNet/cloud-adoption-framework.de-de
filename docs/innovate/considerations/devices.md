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
ms.openlocfilehash: 309ea099eee5fcec5700a48afc4376dbc30805f9
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565652"
---
# <a name="ambient-experiences-interact-with-devices"></a>Umgebungserfahrungen: Interagieren mit Geräten

Unter [Entwickeln von Lösungen mit Blick auf die Kundenanforderungen](./build.md) haben wir die drei Tests wahrer Innovation erörtert: Erfüllung eines Kundenbedürfnisses, dauerhafte Bindung des Kunden und Skalierung in einem Stamm von Kundenkohorten. Jeder Test Ihrer Hypothese erfordert Aufwand und Iterationen hinsichtlich des Ansatzes zur Umsetzung. Dieser Artikel bietet Einblicke in einige weitergehende Ansätze, um diesen Aufwand mittels *Umgebungserfahrungen* zu verringern. Durch die Interaktion mit Geräten statt mit einer Anwendung kann es sein, dass sich der Kunde eher zuerst Ihrer Lösung zuwendet.

## <a name="ambient-experiences"></a>Umgebungserfahrungen

Eine Umgebungserfahrung ist eine digitale Erfahrung in Bezug auf die unmittelbare Umgebung. Eine Lösung mit Umgebungserfahrungen ist darauf ausgerichtet, den Kunden im Moment seines Bedürfnisses zu erreichen. Wenn möglich, erfüllt die Lösung das Kundenbedürfnis, ohne den Ablauf der Aktivität zu verlassen, die sie ausgelöst hat.

Das Leben in der digitalen Wirtschaft ist voller Ablenkungen. Wir alle werden mit Nachrichten, ob visuell oder verbal, aus sozialen Medien, per E-Mail oder dem Internet, bombardiert, von denen jede ein Ablenkungsrisiko darstellt. Dieses Risiko steigt mit jeder Sekunde zwischen dem Zeitpunkt des Bedarfs des Kunden und dem Zeitpunkt, an dem er eine Lösung findet. Unzählige Kunden gehen in dieser kurzen Zeitspanne verloren. Um einen Anstieg wiederholter Akzeptanz zu fördern, müssen Sie die Anzahl der Ablenkungen verringern, indem Sie die Zeit bis zur Lösung verkürzen.

## <a name="interacting-with-devices"></a>Interagieren mit Geräten

Eine standardmäßige Weboberfläche ist die verbreitetste Anwendungsentwicklungstechnik zur Erfüllung von Kundenbedürfnissen. Bei diesem Ansatz wird davon ausgegangen, dass sich der Kunde am Computer befindet. Wenn Ihr Kunde seine Bedürfnisse stets am Laptop erfüllt, entwickeln Sie eine Web-App. Diese Web-App bietet dem Kunden in diesem Szenario eine Umgebungserfahrung. Wir wissen jedoch, dass dieses Szenario in unserer aktuellen Zeit immer seltener und weniger wahrscheinlich wird.

![Umgebungserfahrungen](../../_images/innovate/ambient-experiences.png)

Umgebungserfahrungen erfordern heutzutage in der Regel mehr als eine Web-App. Durch [Messungen](./measure.md) und [Lernen vom Kunden](./learn.md) kann das Verhalten, das zum Bedürfnisauslöser des Kunden führt, beobachtet, verfolgt und genutzt werden, um eine bessere Umgebungserfahrung zu schaffen. In der folgenden Liste werden einige Ansätze zur Einbeziehung von Umgebungslösungen in Ihre Hypothesen zusammengefasst. Weitere Details dazu finden Sie in den folgenden Abschnitten.

- **[Mobiles Erlebnis:](#mobile-experience)** Wie Laptops sind auch mobile Apps in Kundenumgebungen allgegenwärtig. In einigen Situationen kann dies ein ausreichendes Maß an Interaktivität bieten, um eine adäquate Lösung für die Umgebung zu realisieren.
- **[Mixed Reality](#mixed-reality):** Mitunter muss die typische Umgebung eines Kunden geändert werden, um eine entsprechende Interaktion zu ermöglichen. Dadurch wird eine Art falsche Realität geschaffen, in der der Kunde mit der Lösung interagiert und sein Bedürfnis erfüllt werden kann. In diesem Fall ist die Lösung innerhalb der falschen Realität umgebungsgerecht.
- **[Integrierte Realität](#integrated-reality):** Um der tatsächlichen Umgebung näher zu kommen, konzentrieren sich Lösungen für integrierte Realität auf den Einsatz eines Geräts, das in der Realität des Kunden existiert, um die Lösung in seine natürliche Verhaltensweisen einzubinden. Ein virtueller Assistent ist ein gutes Beispiel für die Integration von Realität in die Umgebung. Eine weniger bekannte Option stellt die Nutzung von IoT-Technologien (Internet of Things, Internet der Dinge) zur Einbindung von Geräten dar, die bereits in der Umgebung des Kunden vorhanden sind.
- **[Angepasste Realität](#adjusted-reality):** Wenn für eine dieser Umgebungslösungen eine prädiktive Analyse in der Cloud genutzt wird, um eine Interaktion mit dem Kunden in der natürlichen Umgebung zu definieren und bereitzustellen, zeichnet sich die Lösung durch eine angepasste Realität aus.

Das Erfassen der Kundenbedürfnisse und das Messen der Auswirkung auf den Kunden helfen bei der Entscheidung, ob eine Interaktion mit einem Gerät oder eine Umgebungserfahrung erforderlich ist, um Ihre Hypothese zu bestätigen. Anhand jedes dieser Datenpunkte werden die folgenden Abschnitte Ihnen helfen, die beste Lösung zu finden.

## <a name="mobile-experience"></a>Mobile Erfahrung

Die erste Phase der Umgebungserfahrung stellt das Lösen des Benutzers vom Computer dar. Die heutigen Verbraucher und Geschäftsleute bewegen sich fließend zwischen mobilen Geräten und PCs. Alle von Ihrem Kunden genutzten Plattformen oder Geräte schaffen potenziell eine neue Erfahrung. Das Hinzufügen einer mobilen Erfahrung zur Erweiterung der primären Lösung ist der schnellste Weg, um die Einbindung in die unmittelbare Umgebung des Kunden zu verbessern. Obwohl ein mobiles Gerät weit von einer Umgebungserfahrung entfernt ist, könnte es näher an den Moment des Bedürfnisses des Kunden heranrücken.

Wenn Kunden mobil sind und häufig ihren Standort wechseln, kann dies die relevanteste Form der Umgebungserfahrung für eine bestimmte Lösung sein. Im letzten Jahrzehnt wurden Innovationen häufig durch die Integration vorhandener Lösungen in eine mobile Umgebung ausgelöst.

Azure App Service ist ein gutes Beispiel für diesen Ansatz. Während der ersten Iterationen kann die [Web-App-Funktion von Azure App Service](https://docs.microsoft.com/azure/app-service/overview) zum Testen der Hypothese verwendet werden. Mit zunehmender Komplexität der Hypothesen kann die [mobile App-Funktion von Azure App Services](https://docs.microsoft.com/azure/app-service-mobile) die Web-App so erweitern, dass sie auf einer Vielzahl mobiler Plattformen ausgeführt wird.

## <a name="mixed-reality"></a>Mixed Reality

Mixed Reality-Lösungen stellen die nächste Stufe von Umgebungserfahrungen dar. Bei diesem Ansatz wird die Umgebung des Kunden ergänzt oder repliziert, um die Realität zu erweitern, in der der Kunde agieren kann.

> [!IMPORTANT]
> Wenn ein VR-Gerät (Virtual Reality) benötigt wird und *nicht bereits Teil der unmittelbaren Umgebung oder des natürlichen Verhaltens eines Kunden* ist, dann ist Augmented oder Virtual Reality eher eine alternative Erfahrung als eine Umgebungserfahrung.

Mixed Reality-Umgebungen treten bei mobilen Mitarbeitern im Außendienst immer häufiger auf. Ihr Einsatz steigt noch schneller in Branchen, die Zusammenarbeit oder Fachkompetenz erfordern, die auf dem lokalen Markt nicht ohne Weiteres verfügbar ist. Situationen, in denen eine zentralisierte Implementierungsunterstützung für ein komplexes Produkt für Mitarbeiter an einem entfernten Standort erforderlich ist, bieten sich besonders für Augmented Reality an. In diesen Szenarien können das zentrale Supportteam und der Remotemitarbeiter Augmented Reality einsetzen, um Fehler zu beheben und das Produkt zu installieren.

Betrachten Sie beispielsweise den Fall eines Raumankers. Raumanker ermöglichen Ihnen das Erzeugen von Mixed Reality-Umgebungen mit Objekten, die ihre jeweilige Position im Zeitverlauf geräteübergreifend beibehalten. Durch Raumanker kann ein bestimmtes Verhalten erfasst, aufgezeichnet und beibehalten werden, das eine Umgebungserfahrung bietet, wenn der Benutzer das nächste Mal innerhalb dieser erweiterten Umgebung arbeitet. [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview) ist ein Dienst, der diese Logik in die Cloud verlagert und es ermöglicht, Erfahrungen zwischen Geräten und sogar zwischen Lösungen zu teilen.

## <a name="integrated-reality"></a>Integrierte Realität

Jenseits mobiler Realität oder selbst Mixed Reality liegt die integrierte Realität. Integrierte Realität zielt darauf ab, die digitale Umgebung vollständig aufzuheben. Überall um uns herum befinden sich Geräte mit Compute- und Verbindungsfunktionen. Mit diesen Geräten können Daten aus der unmittelbaren Umgebung erfasst werden, ohne dass der Kunde dafür ein Smartphone, einen Laptop oder ein VR-Gerät bedienen muss.

Diese Erfahrung ist ideal, wenn sich eine bestimmte Art von Gerät stets in der gleichen Umgebung befindet, in der die Kundenbedürfnisse entstehen. Übliche Szenarien sind Fabrikhallen, Aufzüge und sogar Ihr Auto. Diese Art großformatiger Geräte verfügt bereits über Computeleistung. Sie können auch Daten vom Gerät selbst verwenden, um Kundenverhalten zu erkennen und diese Verhaltensweisen in die Cloud zu übertragen. Diese automatische Erfassung von Daten zum Kundenverhalten reduziert die Notwendigkeit der Dateneingabe durch einen Kunden erheblich. Darüber hinaus kann die Web-, mobile oder VR-Erfahrung als Feedbackschleife eingesetzt werden, um auszutauschen, was die Lösung für integrierte Realität gelernt hat.

Beispiele für integrierte Realität in Azure sind u. a.:

- [Azure IoT-Lösungen:](https://docs.microsoft.com/azure/iot-fundamentals) eine Sammlung von Diensten in Azure, die alle bei der Verwaltung von Geräten und dem Fluss von Daten von diesen Geräten in die Cloud und zurück zu Endbenutzern helfen
- [Azure Sphere:](https://docs.microsoft.com/azure-sphere) eine Kombination aus Hardware und Software. Azure Sphere ist eine inhärent sichere Möglichkeit, einem bestehenden Gerät zu ermöglichen, Daten sicher von und zu Azure IoT-Lösungen zu übertragen.
- [Azure Kinect Developer Kit:](https://docs.microsoft.com/azure/Kinect-dk) KI-Sensoren mit erweiterten Modellen für maschinelles Sehen und Sprache. Diese Sensoren können visuelle und Audiodaten aus der unmittelbaren Umgebung erfassen und als Eingaben an Ihre Lösung übermitteln.

Sie können diese drei Tools zum Sammeln von Daten aus der natürlichen Umgebung zum Zeitpunkt der Kundenanforderung verwenden. Anschließend kann Ihre Lösung auf diese Dateneingaben reagieren, um das Bedürfnis zu erfüllen, manchmal bevor der Kunde überhaupt weiß, dass ein Auslöser für dieses Bedürfnis entstanden ist.

## <a name="adjusted-reality"></a>Angepasste Realität

Die höchste Form der Umgebungserfahrung ist die angepasste Realität, die oft als *Umgebungsintelligenz* bezeichnet wird. Angepasste Realität ist ein Ansatz zur Nutzung von Informationen aus Ihrer Lösung, um die Realität des Kunden zu beeinflussen, ohne dass eine direkte Interaktion mit einer Anwendung erforderlich ist. Bei diesem Ansatz ist die Anwendung, die Sie ursprünglich zum Nachweis Ihrer Hypothese entwickelt haben, möglicherweise völlig unwichtig. Stattdessen passen die Geräte in der Umgebung die Ein- und Ausgaben an, um die Bedürfnisse der Kunden zu decken.

Virtuelle Assistenten und intelligente Lautsprecher sind ein gutes Beispiel für angepasste Realität. Allein ist ein intelligenter Lautsprecher ein Beispiel für einfache integrierte Realität. Fügen Sie einer intelligenten Lautsprecherlösung aber einen intelligenten Licht- und Bewegungssensor hinzu, dann ist es ganz einfach, eine einfache Lösung zu schaffen, bei der das Licht beim Betreten eines Raums eingeschaltet wird.

Fabrikhallen auf der ganzen Welt bieten zusätzliche Beispiele für angepasste Realität. In frühen Phasen integrierter Realität erkannten Sensoren von Geräten Bedingungen wie Überhitzung und warnten dann einen menschlichen Bediener über eine Anwendung. Bei der angepassten Realität ist der Kunde möglicherweise weiterhin beteiligt, aber die Feedbackschleife ist enger. In einer Fabrikhalle mit angepasster Realität erkennt ein Gerät eine Überhitzung in einer kritischen Maschine irgendwo an der Montagelinie. An anderer Stelle in der Halle verlangsamt dann ein zweites Gerät die Produktion etwas, damit die Maschine abkühlen kann. Nachdem der Vorfall behoben wurde, wird das Tempo wieder aufgenommen. In dieser Situation spielt der Kunde keine wesentliche Rolle mehr. Der Kunde verwendet Ihre Anwendung, um die Regeln festzulegen und zu verstehen, wie sich diese Regeln auf die Produktion ausgewirkt haben – er ist jedoch kein erforderlicher Teil der Feedbackschleife mehr.

Die in [Azure IoT-Lösungen](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](https://docs.microsoft.com/azure-sphere) und [Azure Kinect Developers Kit](https://docs.microsoft.com/azure/Kinect-dk) beschriebenen Azure-Dienste könnten jeweils Komponenten einer Lösung für angepasste Realität sein. Ihre ursprüngliche Anwendungs- und Geschäftslogik dient dabei als Vermittler zwischen den Eingaben aus der Umgebung und den Änderungen, die an der physischen Umgebung vorgenommen werden müssen.

Ein digitaler Zwilling ist ein weiteres Beispiel für angepasste Realität. Dieser Begriff bezieht sich auf eine digitale Darstellung eines physischen Geräts, das über Computer-, mobile oder Mixed Reality-Formate dargestellt wird. Im Gegensatz zu weniger komplexen 3D-Modellen spiegelt ein digitaler Zwilling Daten wider, die von einem realen Gerät in der physischen Umgebung gesammelt wurden. Diese Lösung ermöglicht dem Benutzer, mit der digitalen Darstellung auf eine Weise zu interagieren, die in der realen Welt unmöglich wäre. Bei diesem Ansatz passen physische Geräte eine Mixed Reality-Umgebung an. Die Lösung sammelt jedoch nach wie vor Daten aus einer Lösung mit integrierter Realität und nutzt diese, um die Realität der aktuellen Umgebung des Kunden zu gestalten.

In Azure dient ein Dienst namens [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins) zum Erstellen von und Zugreifen auf digitale Zwillinge.

## <a name="next-steps"></a>Nächste Schritte

Mit diesem fundierten Verständnis der Interaktionen von Geräten und Umgebungserfahrung, die für Ihre Lösung geeignet ist, sind Sie nun bereit, das abschließende Thema im Bereich Innovation zu erkunden: [Vorhersagen und Beeinflussen](./predict.md).

> [!div class="nextstepaction"]
> [Vorhersagen und Beeinflussen](./predict.md)
