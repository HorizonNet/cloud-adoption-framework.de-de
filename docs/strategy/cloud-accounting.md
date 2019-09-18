---
title: Was ist Cloudbuchhaltung?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erläuterung des Konzepts der Cloudbuchhaltung
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 834beb021b394e2d6ffe58723caced7519923b59
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031124"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>Was ist Cloudbuchhaltung?

Die Cloud verändert, wie die IT-Abteilung Kosten abrechnet, wie unter [Erstellen eines Finanzmodells für die Cloudtransformation](./financial-models.md) beschrieben. Verschiedene IT-Buchhaltungsmodelle werden aufgrund der Art der Abrechnungen von Cloudkosten erheblich vereinfacht. Daher ist es wichtig zu verstehen, wie die Cloudkosten abzurechnen sind, bevor die Cloudtransformation gestartet wird. In diesem Artikel werden die am häufigsten verwendeten Modelle für die Cloudbuchhaltung von IT-Ausgaben erläutert.

## <a name="traditional-it-accounting-cost-center-model"></a>Herkömmliche IT-Buchhaltung (Kostenstellenmodell)

Es ist häufig korrekt, IT als Kostenstelle zu betrachten. Beim herkömmlichen Buchhaltungsmodell für die IT galt diese praktisch als Einkäufer für alle IT-Ressourcen. Wie im Artikel [Finanzmodelle](./financial-models.md) beschrieben, kann diese Zentralisierung des Einkaufs auch Softwarelizenzen, wiederkehrende Gebühren für CRM-Lizenzen, den Erwerb von Mitarbeitercomputern und andere große Ausgaben umfassen.

Wenn die IT als Kostenstelle abgerechnet wird, erfolgt die Bewertung der IT häufig auch aus Sicht des Beschaffungsmanagements. Diese Sichtweise macht es für die Unternehmensleitung schwierig, den tatsächlichen Wert der IT-Abteilung zu beurteilen. Beschaffungskosten verzerren die Sicht auf die IT, da sie andere Werte überdecken, die der Organisation hinzugefügt werden. Aus diesem Grund wird die IT häufig dem CFO oder COO unterstellt. Allerdings ist diese Sichtweise auf die IT sehr beschränkt und kurzsichtig.

## <a name="central-it-accounting-profit-center-model"></a>Zentrale IT-Buchhaltung (Profitcentermodell)

Um die weit verbreitete Ansicht zu überwinden, dass die IT eine reine Kostenstelle darstellt, nutzen einige CIOs ein zentrales IT-Modell für die Buchhaltung. Bei diesem Modell wird die IT-Abteilung wie jede andere Geschäftseinheit behandelt und anhand der generierten Erlöse bewertet. In einigen Fällen ist dieses Modell auch logisch nachvollziehbar. Einige Organisationen haben z. B. eine professionelle IT-Dienstleistungsabteilung, die Erlöse generiert. In vielen Fällen generieren zentrale IT-Modelle keine signifikanten Umsätze, sodass es schwierig ist, das Modell zu rechtfertigen.

Unabhängig vom Umsatzmodell besteht die Besonderheit von zentralen IT-Buchhaltungsmodellen darin, wie die Kosten einer IT-Einheit abgerechnet werden. In einem herkömmlichen IT-Modell erfasst das IT-Team die Kosten und zahlt diese aus den gemeinsamen Geldmitteln (z. B. für Betrieb und Wartung) oder rechnet sie über ein dediziertes Gewinn-und-Verlust-Konto (GuV) ab.

In einem zentralen IT-Buchhaltungsmodell gibt die IT-Abteilung auch die bereitgestellten Dienste an, um den Aufwand, die Verwaltung und andere geschätzte Ausgaben gegenzurechnen. Anschließend werden diese Kosten bei der jeweils angegebenen Geschäftseinheit in Rechnung gestellt. In diesem Modell wird davon ausgegangen, dass der IT-Abteilungsleiter (CIO) die GuV im Zusammenhang mit dem Verkauf dieser Dienste verwaltet. Dies kann zu einem erheblichen Anstieg der IT-Kosten und zu Konflikten zwischen der zentralen IT-Abteilung und anderen Geschäftsbereichen führen, insbesondere dann, wenn die IT die Kosten senken muss oder vereinbarte SLAs nicht erfüllt. Während Änderungen an Technologien oder Markten könnte jede neue Technologie eine Störung in der GuV der zentralen IT bedeuten und damit die Transformation schwieriger machen.

## <a name="chargeback"></a>Chargeback (verbrauchsbasierte Kostenzuteilung)

Einen der allgemein ersten Schritte bei der Verbesserung der Reputation der IT-Abteilung als Kostenstelle stellt die Einführung eines Buchhaltungsmodells mit verbrauchsbasierter Kostenzuteilung dar. Dieses Modell gilt insbesondere in kleineren Unternehmen und hocheffizienten IT-Organisationen. Beim Modell mit verbrauchsbasierter Kostenzuteilung werden alle IT-Kosten, die einer bestimmten Geschäftseinheit zugeordnet sind, im Budget der Unternehmenseinheit wie Betriebsausgaben behandelt. Diese Praxis reduziert die kumulierten Kostenauswirkungen auf die IT, sodass Geschäftswerte deutlicher erkennbar sind.

In einem traditionellen – lokalen – Modell ist eine verbrauchsbasierte Kostenzuteilung schwer umzusetzen, da jemand die großen Kapitalausgaben und Abschreibungen übernehmen muss. Ein laufender Wechsel von Kapitalausgaben zu Betriebsausgaben nach Verbrauch ist für die Buchhaltung eine schwierige Aufgabe. Diese Schwierigkeit ist ein wichtiger Grund für das herkömmliche Buchhaltungsmodell für die IT und das Modell mit zentraler IT-Abrechnung. Für eine effiziente Umsetzung eines Modells mit verbrauchsbasierter Kostenzuteilung ist fast zwangsläufig ein Modell mit Betriebsausgaben für die Abrechnung von Cloudkosten erforderlich.

Sie sollten dieses Modell jedoch nicht implementieren, ohne die Auswirkungen zu berücksichtigen. Hier finden Sie einige Auswirkungen, die nur das Modell mit verbrauchsbasierter Kostenzuteilung verursacht:

- Die verbrauchsbasierte Kostenzuteilung führt zu einer enormen Verringerung des gesamten IT-Budgets. Für IT-Organisationen, die ineffizient sind oder bei Betrieb oder Wartung umfassende komplexe IT-Qualifikationen benötigen, können diese Ausgaben in diesem Modell fehlerhaft widergespiegelt werden.
- Eine häufige Folge ist der Verlust der Kontrolle. In sehr politischen Umgebungen kann die verbrauchsbasierte Kostenzuteilung zu einem Verlust der Kontrolle und zur Versetzung von Mitarbeitern im Unternehmen führen. Dies kann erhebliche Einschränkungen verursachen und verhindern, dass die IT Projektanforderungen oder SLAs konsistent einhält.
- Schwierigkeiten bei der Abrechnung gemeinsamer Dienste sind eine weitere häufige Folge. Wenn die Organisation durch eine Übernahme gewachsen ist und aus diesem Grund technische Schulden hat, gibt es wahrscheinlich einen hohen Prozentsatz an gemeinsamen Diensten, die beibehalten werden müssen, damit alle Systeme effektiv zusammenarbeiten können.

Cloudtransformationen umfassen Lösungen für diese und andere Folgen des Modells zur verbrauchsbasierten Kostenzuteilung. Aber jede dieser Lösungen schließt Implementierungs- und Betriebskosten ein. CIO und CFO sollten die Vor- und Nachteile eines Modells für die verbrauchsbasierte Kostenzuteilung abwägen, bevor dieses Modell in Betracht gezogen wird.

## <a name="showback-or-awareness-back"></a>Showback oder Awarenessback

Für größere Unternehmen ist ein Showbackmodell meist der sicherere erste Schritt beim Übergang von Kostenstellen zu Wertstellen. Dieses Modell wirkt sich nicht auf die Finanzbuchhaltung aus. Tatsächlich bleibt die GuV der meisten Organisationen unverändert. Die größte Umstellung erfolgt bei der Haltung und dem Bewusstsein. Beim Showbackmodell verwaltet die IT die zentralisierte und konsolidierte Beschaffung als Agent für das Unternehmen. In Berichten an die Geschäftsleitung ordnet die IT alle direkten Kosten den entsprechenden Geschäftseinheiten zu und senkt dadurch das für die IT-Abteilung wahrgenommene Budget. Außerdem plant die IT so auch Budgets nach den Anforderungen der zugeordneten Geschäftseinheiten, sodass die IT-Abteilung Kosten, die ausschließlich IT-Initiativen zugeordnet sind, genauer abrechnen kann.

Dieses Modell bietet eine Balance zwischen einem echten Modell mit verbrauchsbasierter Kostenzuteilung und herkömmlicheren Modellen für die IT-Buchhaltung.

## <a name="impact-of-cloud-accounting-models"></a>Auswirkungen der Modelle für die Cloudbuchhaltung

Die Auswahl des Buchhaltungsmodells ist für den Systementwurf entscheidend. Das ausgewählte Buchhaltungsmodell kann sich auf Abonnementstrategien, Benennungsstandards, Kennzeichnungsstandards und die Entwürfe für Richtlinien und Blaupausen auswirken.

Nachdem Sie zusammen mit der Geschäftsführung Entscheidungen zu einem Modell für die Cloudbuchhaltung und die [globalen Märkte](./global-markets.md) getroffen haben, verfügen Sie über genügend Informationen zum [Entwickeln eines Azure-Fundaments](../ready/index.md).

> [!div class="nextstepaction"]
> [Entwickeln eines Azure-Fundaments](../ready/index.md)
