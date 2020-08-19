---
title: Beispiele für Agilitätsergebnisse
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit der Marktposition Ihres Unternehmens und seinen Wettbewerbern vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 1df64e7777e045f0e52871ac04b243e4c3b3902d
ms.sourcegitcommit: 949b87bad28d32df84df190160089f01826f3a31
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88194528"
---
# <a name="examples-of-agility-outcomes"></a>Beispiele für Agilitätsergebnisse

Wie bereits in der [Übersicht über die Geschäftsergebnisse](./index.md) beschrieben, können mehrere mögliche Geschäftsergebnisse als Grundlage für Unterhaltungen zur Transformationsjourney mit dem Unternehmen dienen. In diesem Artikel konzentrieren wir uns auf eine gängige Geschäftskennzahl: die Unternehmensflexibilität. Kenntnisse der Marktposition Ihres Unternehmens und der Wettbewerber können Ihnen dabei helfen, die Geschäftsergebnisse als Ziel der Transformationsjourney des Unternehmens zu formulieren.

In der Vergangenheit wurden Chief Investment Officers und IT-Teams als eine Säule für die Stabilität zentraler unternehmenskritischer Prozesse angesehen. Dies gilt auch weiterhin. Nur wenige Unternehmen funktionieren gut, wenn ihre IT-Plattform nicht stabil ist. Allerdings wird in der heutigen Geschäftswelt noch viel mehr erwartet. Die IT kann mehr als nur eine weitere Kostenstelle sein, indem sie mit anderen Bereichen kooperiert, um neue Möglichkeiten am Markt zu erschließen. Viele Chief Investment Officers und Führungskräfte setzen die Stabilität einfach als Grundwerte für die IT voraus. Für diese Führungskräfte ist geschäftliche Flexibilität das Maß für den Anteil der IT am Unternehmen.

## <a name="why-is-agility-so-important"></a>Warum ist Agilität so wichtig?

Die Märkte verändern sich heute schneller als bisher. 2015 waren nur noch 57 Unternehmen in den Fortune 500, die auch 61 Jahre zuvor zu diesem Kreis gehörten – das entspricht einer Fluktuation von 88,6 Prozent. Dies zeigt, dass sich die Märkte mit einer bisher nicht vorstellbaren Geschwindigkeit wandeln. Flexibilität bei der IT oder sogar dem gesamten Unternehmen haben sicherlich keine direkten Auswirkungen auf die Einordnung einer Organisation in die Fortune 500-Unternehmen, diese Zahlen helfen uns aber dennoch dabei, die Geschwindigkeit, mit der sich die Märkte auch weiterhin verändern, besser zu verstehen.

Für etablierte und neue Unternehmen kann geschäftliche Flexibilität gleichermaßen den Unterschied zwischen Erfolg oder Misserfolg einer Geschäftsinitiative bedeuten. Die schnelle Anpassung an Marktveränderungen kann dazu beitragen, Bestandskunden zu halten oder Marktanteile von Wettbewerbern zu gewinnen. Mit den agilitätsbezogenen Ergebnissen in den nächsten Abschnitten kann der Wert der Cloud während einer Transformation kommuniziert werden.

## <a name="time-to-market-outcome"></a>Ergebnis für die Markteinführungszeit

Bei allen Bemühungen zu cloudfähigen Innovationen ist die Zeit bis zur Markteinführung ein wichtiges Maß zur Bewertung der Fähigkeit einer IT-Abteilung, auf Marktveränderungen zu reagieren. In vielen Fällen verfügt ein Manager möglicherweise über ein Budget für die Erstellung einer Anwendung oder die Einführung eines neuen Produkts. Klare Angaben zum Vorteil der Markteinführungszeit kann solche Führungskräfte motivieren, ein Budget für die Transformationsjourney der IT freizugeben.

- **Beispiel 1:** Die europäische Abteilung einer in den USA ansässigen Firma muss zur Einhaltung der DSGVO-Vorschriften die Kundendaten in einer Datenbank für die eigenen Geschäfte in Großbritannien schützen. Ihre vorhandene Version von SQL Server unterstützt die erforderliche Sicherheit auf Zeilenebene nicht. Ein direktes Upgrade würde zu viele Unterbrechungen bedeuten. Durch die Verwendung von Azure SQL-Datenbank für Replikation und Upgrade der Datenbank implementiert der Kunde die erforderlichen Compliancemaßnahmen innerhalb weniger Wochen.

- **Beispiel 2:** Ein Logistikunternehmen hat ein bisher nicht bedientes Marktsegment gefunden, benötigt aber eine neue Version der eigenen Flagship-Anwendung, um in dieses vorzudringen. Ein größerer Mitbewerber hat dies ebenfalls erkannt. Durch eine cloudfähige Anwendungsinnovation begeistert das Unternehmen die Kunden und ist durch einen DevOps-Entwicklungsansatz in der Lage, den langsameren und älteren Konkurrenten um *x* Monate zu schlagen. Dieser Sprung beim Markteinstieg sichert den Kundenstamm.

<!-- docsTest:ignore "Jamey Shiels" "Vice President of Digital Experience" "Aurora Health Care" -->

### <a name="aurora-health-care"></a>Aurora Health Care

Das Gesundheitssystem transformiert Onlinedienste in ein freundliches digitales Erlebnis. Zum Transformieren der eigenen digitalen Dienste migriert Aurora Health Care seine Websites zur Microsoft Azure-Plattform und setzt auf eine Strategie fortlaufender Innovationen.

<!-- cSpell:ignore Jamey Shiels -->

> „Als Team fokussieren wir uns auf hochwertige Lösungen und hohe Geschwindigkeit. Die Entscheidung für Azure war für uns eine riesige Veränderung.“
>
> Jamey Shiels
>
> Vice President für digitale Ressourcen bei
>
> Aurora Health Care

## <a name="provision-time"></a>Bereitstellungszeit

Wenn Geschäfte neue IT-Dienste oder eine Skalierung vorhandener Dienste erfordern, kann die Beschaffung und Bereitstellung neuer Hardware oder virtueller Ressourcen Wochen dauern. Nach der Migration zur Cloud kann die IT-Abteilung problemlos Self-Service-Bereitstellung ermöglichen, mit denen das Unternehmen Skalierungen innerhalb von Stunden durchführen kann.

- **Beispiel:** Ein Unternehmen für Verbrauchsgüter muss pro Jahr Hunderte von Datenbankclustern erstellen und entfernen, um die betrieblichen Anforderungen des Unternehmens zu erfüllen. Die lokalen virtuellen Hosts können zwar schnell bereitgestellt werden, aber die Wiederherstellung virtueller Ressourcen ist langsam und damit sehr zeitaufwendig für das Team. Daher ist die lokale Umgebung viel zu groß und kann nur selten mit dem Bedarf Schritt halten. Nach der Migration zur Cloud kann die IT-Abteilung viel einfacher eine skriptgesteuerte Self-Service-Bereitstellung von Ressourcen ermöglichen und dabei für die Abrechnung einen Ansatz mit verbrauchsbasierter Kostenzuteilung nutzen. Zusammen kann das Unternehmen Änderungen damit so schnell wie nötig umsetzen und trotzdem die Kosten für die benötigten Ressourcen in einem verantwortungsvollen Rahmen halten. Mit der Umsetzung in der Cloud werden die Bereitstellungen lediglich durch das Unternehmensbudget beschränkt.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über [Reichweitenergebnisse](./reach-outcomes.md).

> [!div class="nextstepaction"]
> [Reichweitenergebnisse](./reach-outcomes.md)
