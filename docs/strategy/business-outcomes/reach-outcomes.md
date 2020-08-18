---
title: Beispiele für globale Reichweitenergebnisse
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Reichweitenergebnissen in Bezug auf die Cloudtransformation vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 400c1edef752621adbde85ee26cca2445a3367af
ms.sourcegitcommit: d31a9043d1ae9283ed126bf118ca26d1d18d6948
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88040924"
---
<!-- cSpell:ignore Personalizer -->
<!-- docsTest:ignore "global reach" -->

# <a name="examples-of-global-reach-outcomes"></a>Beispiele für globale Reichweitenergebnisse

Wie bereits in den [Geschäftsergebnissen](./index.md) beschrieben, können mehrere mögliche Geschäftsergebnisse als Grundlage für Unterhaltungen zur Transformationsjourney mit dem Unternehmen dienen. In diesem Artikel konzentrieren wir uns auf eine gängige Geschäftskennzahl: Reichweite. *Reichweite* ist ein präziser Begriff, der sich in diesem Fall auf die Globalisierungsstrategie eines Unternehmens bezieht. Kenntnisse der Globalisierungsstrategie des Unternehmens helfen Ihnen dabei, die Geschäftsergebnisse als Ziel der Transformationsjourney eines Unternehmens zu formulieren.

Fortune 500-Unternehmen und kleinere Unternehmen fokussieren sich seit mehr als drei Jahrzehnten auf die Globalisierung von Diensten und Kunden, und die meisten Unternehmen sind wahrscheinlich am globalen Handel beteiligt, da die Globalisierung weiterhin im Fokus steht. Das Hosting von Rechenzentren auf der ganzen Welt kann mehr als 80 Prozent des jährlichen IT-Budgets beanspruchen, und große Netzwerke, die private Leitungen zum Verbinden dieser Rechenzentren verwenden, können Millionen von Dollar pro Jahr Kosten. Die Unterstützung globaler Geschäfte ist daher schwierig und teuer.

Bei Cloudlösungen werden die Kosten für die Globalisierung an den Cloudanbieter weitergegeben. In Azure können Kunden Ressourcen sehr schnell in derselben Region wie die Kunden oder Geschäfte bereitstellen, ohne ein Rechenzentrum kaufen und bereitstellen zu müssen. Microsoft besitzt eines der größten Fernnetze (WAN) der Welt, über das Rechenzentren auf der ganzen Welt miteinander verbunden sind. Konnektivität und globale Kapazitäten stehen globalen Kunden bei Bedarf zur Verfügung.

## <a name="global-access"></a>Globaler Zugang

Die Erschließung eines neuen Markts kann während einer Transformation eines der wichtigsten Geschäftsergebnisse sein. Durch die Möglichkeit einer schnellen Bereitstellung von Ressourcen ohne längerfristige Verpflichtung in einem Markt können leitende Vertriebs- und Betriebsmitarbeiter Optionen erkunden, die in der Vergangenheit nicht einmal in Erwägung gezogen worden wären.

### <a name="example"></a>Beispiel

Ein Kosmetikhersteller hat einen Trend entdeckt. Einige Produkte werden in die Region Asien-Pazifik geliefert, obwohl dort keine Vertriebsteams arbeiten. Die Mindestanforderungen an die Systeme für Außendienstmitarbeiter sind zwar niedrig, aber die Latenz verhindert eine RAS-Lösung. Der Vice President des Vertriebsteams möchte ein Experiment mit Vertriebsteams in Japan und Südkorea starten, um trotzdem von diesem Trend profitieren zu können. Da das Unternehmen bereits zur Cloud migriert ist, konnte es die erforderlichen Systeme in Japan und Südkorea innerhalb weniger Tage bereitstellen. So konnte der Vertriebsleiter den Umsatz in der Region innerhalb von drei Monaten um _x %_ steigern. Diese beiden Märkte übertreffen andere Regionen auf der Welt auch weiterhin und führen zu Vertriebschancen in der gesamten Region.

### <a name="example"></a>Beispiel

Ein Onlinehändler, der Produkte global versendet, kann mit seinen Kunden in verschiedenen Zeitzonen und in mehreren Sprachen zusammenarbeiten. Der Einzelhändler verwendet den Azure Bot Service und verschiedene Features in Azure Cognitive Services wie beispielsweise Übersetzer, Language Understanding (LUIS), den QnA Maker und die Textanalyse. So erhalten Kunden die benötigten Informationen zum richtigen Zeitpunkt in ihrer Sprache. Der Einzelhändler nutzt die [Personalisierung](https://azure.microsoft.com/services/cognitive-services/personalizer/), um die Benutzeroberfläche und die Katalogangebote nach den regionalen Vorlieben der Kunden weiter anzupassen und die Verfügbarkeit sicherzustellen.

## <a name="data-sovereignty"></a>Datenhoheit

Die Erschließung neuer Märkte führt auch zu neuen Governanceeinschränkungen. Azure bietet Complianceangebote, die Kunden dabei helfen, Compliancevorgaben in regulierten Branchen und globalen Märkten zu erfüllen. Weitere Informationen finden Sie in der [Übersicht über Microsoft Azure-Compliance](https://azure.microsoft.com/overview/trusted-cloud/compliance).

### <a name="example"></a>Beispiel

Ein US-Versorgungsunternehmen erhielt einen Vertrag für Einrichtungen in Kanada. Die kanadischen Gesetze zur Datenhoheit erfordern, dass kanadische Daten in Kanada bleiben. Das Unternehmen hatte schon seit Jahren an cloudfähigen Anwendungsinnovationen gearbeitet. Daher wurde die Software des Unternehmens über vollständig skriptgesteuerte DevOps-Prozesse bereitgestellt. Mit wenigen kleinen Änderungen an der Codebasis konnten sie eine Arbeitskopie des Codes in einem Azure-Rechenzentrum in Kanada bereitstellen und damit die Complianceanforderung zur Datenhoheit erfüllen und den Kunden halten.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Kundenbindungsergebnisse.

> [!div class="nextstepaction"]
> [Kundenbindungsergebnisse](./engagement-outcomes.md)
