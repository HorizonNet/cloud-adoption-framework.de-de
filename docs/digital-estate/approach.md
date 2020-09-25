---
title: Ansätze für die Planung digitaler Ressourcen
description: Hier finden Sie grundlegende Informationen zu den Merkmalen und Anforderungen des workloadorientierten, ressourcenorientierten und inkrementellen Top-Down-Ansatzes für die Planung digitaler Ressourcen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 88f0f56507290666aead6e81e10d0a50f7dcae61
ms.sourcegitcommit: 4e12d2417f646c72abf9fa7959faebc3abee99d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90774067"
---
# <a name="approaches-to-digital-estate-planning"></a>Ansätze für die Planung digitaler Ressourcen

Die Planung digitaler Ressourcen kann je nach gewünschten Ergebnissen und Größe der vorhandenen Ressourcen auf unterschiedlichste Weise erfolgen. Es gibt verschiedene Ansätze, die Sie wählen können. Es ist wichtig, die Erwartungen in Bezug auf den Ansatz in den frühen Planungszyklen festzulegen. Unklare Erwartungen führen häufig zu Verzögerungen bei weiteren Bestandserfassungen. In diesem Artikel werden drei Ansätze für die Analyse beschrieben.

## <a name="workload-driven-approach"></a>Workloadorientierter Ansatz

Der Ansatz der Top-Down-Bewertung wertet Sicherheitsaspekte aus. Die Sicherheit umfasst die Kategorisierung von Daten (hohe, mittlere oder geringe geschäftliche Auswirkung), Compliance, Datenhoheit und Sicherheitsrisikoanforderungen. Bei diesem Ansatz wird die Komplexität der Architektur auf hoher Ebene bewertet. Sie wertet Aspekte wie Authentifizierung, Datenstruktur, Latenzanforderungen, Abhängigkeiten und Lebenserwartung von Anwendungen aus.

Der Top-Down-Ansatz misst auch die operativen Anforderungen der Anwendung, z.B. Serviceebenen, Integration, Wartungsfenster, Überwachung und Erkenntnisse. Nachdem diese Aspekte analysiert und berücksichtigt wurden, spiegelt das Ergebnis die relative Schwierigkeit der Anwendungsmigration für die einzelnen Cloudplattformen wider: IaaS, PaaS und SaaS.

Die Top-Down-Bewertung beurteilt außerdem den finanziellen Nutzen der Anwendung, z.B. die betriebliche Effizienz, die Gesamtkosten, die Rendite und andere zweckmäßige finanzielle Metriken. Die Bewertung untersucht auch die Saisonalität der Anwendung (beispielsweise Jahreszeiten mit Bedarfsspitzen) und die allgemeine Computeauslastung.

Darüber hinaus werden die unterstützten Benutzertypen (gelegentliche Nutzer/Experten, immer/gelegentlich angemeldete Benutzer) sowie die erforderliche Skalierbarkeit und Elastizität überprüft. Abschließend werden bei der Bewertung die Anforderungen an die Geschäftskontinuität und Resilienz sowie Abhängigkeiten für die Ausführung der Anwendung im Fall einer Dienstunterbrechung geprüft.

> [!TIP]
> Dieser Ansatz erfordert Gespräche mit geschäftlichen und technischen Projektbeteiligten sowie individuelles Feedback zu ihren Erfahrungen. Die Verfügbarkeit der entscheidenden Personen ist das größte Risiko für die zeitliche Planung. Die Tatsache, dass die Datenquellen auf konkreten Daten beruhen, erschwert die Erstellung genauer Kosten- oder Zeitschätzungen. Planen Sie Zeitpläne frühzeitig, und überprüfen Sie alle erfassten Daten.

## <a name="asset-driven-approach"></a>Ressourcenorientierter Ansatz

Der ressourcenorientierte Ansatz liefert einen Plan, der auf den Ressourcen beruht, die die Migration einer Anwendung unterstützen. Bei diesem Ansatz werden statistische Nutzungsdaten aus einer Konfigurationsverwaltungsdatenbank (Configuration Management Database, CMDB) oder anderen Tools zur Infrastrukturbewertung abgerufen.

Der Ansatz setzt in der Regel ein IaaS-Bereitstellungsmodell als Basis voraus. Bei diesem Prozess wertet die Analyse die Attribute jeder Ressource aus: Arbeitsspeicher, Anzahl von Prozessoren (CPU-Kerne), Speicherplatz für das Betriebssystem, Datenlaufwerke, Netzwerkschnittstellenkarten (NICs), IPv6, Netzwerklastenausgleich, Clustering, Betriebssystemversion, Datenbankversion (falls erforderlich), unterstützte Domänen, Komponenten oder Softwarepakete von Drittanbietern usw. Die von Ihnen bei diesem Ansatz inventarisierten Ressourcen werden dann zur Gruppierung und Abhängigkeitszuordnung mit Workloads oder Anwendungen abgeglichen.

> [!TIP]
> Dieser Ansatz erfordert eine umfassende Quelle von statistischen Nutzungsdaten. Die erforderliche Zeit zur Überprüfung des Bestands und Erfassung von Daten stellt das größte Risiko bei der zeitlichen Planung dar. Bei den Datenquellen auf niedriger Ebene können Abhängigkeiten zwischen Ressourcen oder Anwendungen fehlen. Planen Sie mindestens einen Monat für die Überprüfung des Bestands ein. Überprüfen Sie Abhängigkeiten vor der Bereitstellung.

## <a name="incremental-approach"></a>Inkrementeller Ansatz

Wir empfehlen dringend einen inkrementellen Ansatz, wie dies bei vielen Prozessen im Cloud Adoption Framework der Fall ist. Im Fall der Planung digitaler Ressourcen ergibt sich daraus ein mehrstufiger Prozess:

- **Anfängliche Kostenanalyse:** Falls eine finanzielle Prüfung erforderlich ist, beginnen Sie mit dem oben beschriebenen ressourcenorientierten Ansatz, um eine erste Kostenberechnung ohne Rationalisierung für sämtliche digitalen Ressourcen durchzuführen. Dadurch erhalten Sie eine Benchmark für das Worst-Case-Szenario.

- **Migrationsplanung:** Nachdem Sie ein Cloudstrategieteam zusammengestellt haben, erstellen Sie ein anfängliches Migrationsbacklog mithilfe eines workloadbasierten Ansatzes, der auf dem kollektiven Wissen des Teams und den Erkenntnissen aus Gesprächen mit einer begrenzten Anzahl von Projektbeteiligten beruht. Mit diesem Ansatz erhalten Sie schnell eine einfache Workloadbewertung zur Förderung der Zusammenarbeit.

- **Releaseplanung:** Bei jedem neuen Release wird das Migrationsbacklog gelöscht, und die Prioritäten werden erneut auf die wichtigsten geschäftlichen Auswirkungen ausgerichtet. Während dieses Vorgangs werden die nächsten fünf bis zehn Workloads als priorisierte Releases ausgewählt. An diesem Punkt investiert das Cloudstrategieteam Zeit in die Durchführung eines umfassenden workloadorientierten Ansatzes. Wenn diese Bewertung bis zur Abstimmung eines Releases verzögert wird, kommt dies den Projektbeteiligten im Hinblick auf ihren Zeitaufwand entgegen. Außerdem werden die vollständige Analyse und der damit einhergehende Aufwand hinausgezögert, bis die Ergebnisse der ersten Aktivitäten für das Unternehmen erkennbar sind.

- **Ausführungsanalyse:** Bevor Sie eine Ressource migrieren, modernisieren oder replizieren, sollten Sie sie jeweils einzeln und als Teil eines kollektiven Release bewerten. Zu diesem Zeitpunkt können die Daten aus dem ursprünglichen ressourcenorientierten Ansatz untersucht werden, um genaue Angaben zur Dimensionierung und zu den betrieblichen Einschränkungen sicherzustellen.

> [!TIP]
> Dieser inkrementelle Ansatz ermöglicht eine optimierte Planung und führt schneller zu Ergebnissen. Es ist wichtig, dass alle Projektbeteiligten den Ansatz der verzögerten Entscheidungsfindung verstehen. Ebenso wichtig ist es, dass die in den einzelnen Phasen getroffenen Annahmen dokumentiert werden, damit keine Informationen verloren gehen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem ein Ansatz ausgewählt wurde, kann der Bestand erfasst werden.

> [!div class="nextstepaction"]
> [Gather inventory data](./inventory.md) (Erfassen von Bestandsdaten)
