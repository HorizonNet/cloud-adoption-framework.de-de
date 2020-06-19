---
title: Ausrichten des Aufwands auf Lernmetriken
description: Es wird beschrieben, wie Sie Maßnahmen darauf ausrichten, dass die Auswirkung einer Transformation auf das Geschäft gemessen und entsprechend kommuniziert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: d403a16abd441c7698fb4f6ec66328d37641d806
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84786193"
---
# <a name="how-can-we-align-efforts-to-meaningful-learning-metrics"></a>Ausrichtung des Aufwands auf sinnvolle Lernmetriken

In der [Übersicht über die Geschäftsergebnisse](./business-outcomes/index.md) wurden Methoden zum Messen und Kommunizieren der Auswirkungen einer Transformation auf das Geschäft erläutert. Leider können einige dieser Ergebnisse Jahre dauern, bevor messbare Ergebnisse erzielt werden. Das Management und die Unternehmensleitung sind nicht zufrieden mit Berichten, die ein Delta von 0 % über einen längeren Zeitraum aufweisen.

Mit Lernmetriken sind vorläufige kurzfristigere Metriken, die an längerfristige Geschäftsergebnisse gebunden werden können. Diese Metriken eignen sich auch gut für eine wachstumsorientierte Ausrichtung und die Umsetzung von mehr Stabilität. Statt auf dem Fehlen eines zu erwartenden Fortschritts in Bezug auf ein langfristiges Unternehmensziel liegt der Fokus von Lernmetriken auf ersten Anzeichen von Erfolg. Außerdem zeigen die Metriken auch frühe Anzeichen für Fehler auf, die wahrscheinlich die beste Möglichkeit für Sie zum Lernen und Anpassen des Plans darstellen.

Wie bei einem Großteil der Materialien in diesem Framework gehen wir davon aus, dass Sie mit der [Transformationsjourney](../govern/guides/index.md) vertraut sind, die Ihren gewünschten Geschäftsergebnissen am besten entspricht. In diesem Artikel werden einige Lernmetriken für jede Transformationsjourney gezeigt, um das Konzept zu veranschaulichen.

## <a name="cloud-migration"></a>Cloudmigration

Bei dieser Transformation liegt der Schwerpunkt auf Kosten, Komplexität und insbesondere dem IT-Betrieb. Am einfachsten können bei dieser Transformation Daten zum Verschieben von Ressourcen in die Cloud gemessen werden. Bei dieser Art von Transformation wird der digitale Status anhand der virtuellen Computer (VMs), der Racks oder Cluster zum Hosten dieser VMs, der Betriebskosten für das Rechenzentrum, der erforderlichen Kapitalausgaben für das Verwalten von Systemen und der Abschreibung dieser Ressourcen im Lauf der Zeit gemessen.

Mit dem Verschieben der virtuellen Computer in die Cloud wird die Abhängigkeit von den alten lokalen Ressourcen geringer. Die Kosten für die Ressourcenwartung reduzieren sich ebenfalls. Leider können Unternehmen diese Reduzierung der Kosten erst realisieren, wenn die Bereitstellung der Cluster aufgehoben wurde und die Leasedauer des Rechenzentrums abgelaufen ist. In vielen Fällen wird der vollständige Wert des Aufwands erst realisiert, wenn die Abschreibungszyklen abgeschlossen sind.

Vor einem Finanzbericht sollte stets der CFO oder die Finanzabteilung konsultiert werden. Allerdings können IT-Teams im Allgemeinen die aktuellen und zukünftigen Kosten für jeden virtuellen Computer basierend auf CPU, Arbeitsspeicher und verbrauchtem Speicher schätzen. Anschließend können Sie diesen Wert auf jeden migrierten virtuellen Computer anwenden, um die unmittelbaren Kosteneinsparungen und den zukünftigen monetären Nutzen des Aufwands zu schätzen.

## <a name="application-innovation"></a>Anwendungsinnovationen

Innovationen bei cloudfähigen Anwendungen beziehen sich hauptsächlich auf die Benutzerfreundlichkeit und die Bereitschaft der Kunden, Produkte und Dienste des Unternehmens zu nutzen. Es dauert eine Weile, bis der Einfluss einzelner Änderungsschritte auf das Kaufverhalten von Verbrauchern oder Kunden sichtbar wird. Anwendungsinnovationszyklen sind aber in der Regel deutlich kürzer als bei anderen Formen der Transformation. Traditionell wird empfohlen, sich zunächst mit speziellen Verhaltensweisen zu beschäftigen, die Sie beeinflussen möchten, und diese als Lernmetriken zu verwenden. Bei einer E-Commerce-Anwendung könnten z. B. die Gesamteinkäufe oder Zusatzkäufe als Zielverhalten genutzt werden. Für ein Videounternehmen könnte die mit der Wiedergabe eines Videostreams verbrachte Zeit wichtig sein.

Die Herausforderung bei Metriken zum Kundenverhalten besteht darin, dass sie einfach von externen Variablen beeinflusst werden können. Aus diesem Grund ist es häufig wichtig, neben Lernmetriken noch andere verwandte Statistiken einzubeziehen. Solche verwandten Statistiken können z. B. Releaserhythmus, pro Release behobene Fehler, Code Coverage für Komponententests, Anzahl der Seitenaufrufe, Seitendurchsatz, Seitenladevorgänge und andere Leistungsindikatoren für die App sein. Jede kann andere Aktivitäten oder Änderungen an der Codebasis oder der Kundenerfahrung zeigen, die dann mit allgemeineren Verhaltensmustern der Kunden abgeglichen werden können.

## <a name="data-innovation"></a>Dateninnovationen

Der Wechsel einer Branche, das Durchbrechen von Märkten oder das Transformieren von Produkten und Diensten kann Jahre dauern. Bei einer Dateninnovationen unter Einbeziehung einer Cloud ist das Experimentieren ausschlaggebend für messbare Erfolge. Seien Sie transparent, indem Sie Vorhersagemetriken wie Wahrscheinlichkeit in Prozent, Anzahl der fehlerhaften Experimente und Anzahl der trainierten Modelle freigeben. Fehler sammeln sich schneller an als Erfolge. Diese Metriken können entmutigend sein, und das ausführende Team muss nachvollziehen können, welcher Zeitaufwand und welche Investitionen erforderlich sind, um diese Metriken richtig zu nutzen.

Auf der anderen Seite werden einige positive Indikatoren häufig dem datengesteuerten Lernen zugeordnet: Zentralisierung heterogener Datasets, Dateneingang und Datendemokratisierung. Während das Team etwas über die Kunden von morgen lernt, können schon heute greifbare Ergebnisse erzielt werden. Hilfreiche Lernmetriken sind z. B.:

- Anzahl der verfügbaren Modelle
- Anzahl der genutzten Partnerdatenquellen
- Geräte, die eingehende Daten erzeugen
- Eingehende Datenmenge
- Datentypen

Eine noch wichtigere Metrik ist die Anzahl von Dashboards, die anhand der kombinierten Datenquellen erstellt wurden. Diese Anzahl spiegelt die Geschäftsprozesse mit einem aktuellen Status wider, die von neuen Datenquellen betroffen sind. Wenn Sie neue Datenquellen häufig freigeben, kann Ihr Unternehmen die Daten mithilfe von Berichtstools wie Power BI nutzen, um inkrementelle Erkenntnisse zu gewinnen und geschäftsbezogene Änderungen besser voranzubringen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die Lernmetriken abgestimmt wurden, können Sie damit beginnen, mithilfe dieser Metriken das [Geschäftsszenario zu erarbeiten](./cloud-migration-business-case.md).

> [!div class="nextstepaction"]
> [Erarbeiten des Cloudgeschäftsszenarios](./cloud-migration-business-case.md)
