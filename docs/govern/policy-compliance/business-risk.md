---
title: Verstehen des Geschäftsrisikos während der Cloudmigration
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über Risikomanagementprozesse zu informieren, die Ihnen dabei helfen, Migrationsrisiken zu bewerten, zu verstehen, abzuwägen und zu mindern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 07c7534397f2664113cae33b66ca635766f6eb11
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862312"
---
<!-- markdownlint-disable MD026 -->

# <a name="understand-business-risk-during-cloud-migration"></a>Verstehen des Geschäftsrisikos während der Cloudmigration

Ein Überblick über die Geschäftsrisiken ist einer der wichtigsten Aspekte bei der Cloudtransformation. Das Risiko bestimmt die Richtlinien und beeinflusst die Anforderungen an deren Überwachung und Durchsetzung. Das Risiko wirkt sich stark auf die Verwaltung der digitalen Umgebung aus, ob lokal oder in der Cloud.

<!-- markdownlint-enable MD026 -->

## <a name="relativity-of-risk"></a>Relativität von Risiken

Risiken sind relativ. Ein kleines Unternehmen mit ein paar IT-Ressourcen in einem geschlossenen Gebäude ist einem sehr geringen Risiko ausgesetzt. Fügen Sie Benutzer und eine Internetverbindung mit Zugriff auf diese Ressourcen hinzu, und das Risiko wächst. Wenn dieses kleine Unternehmen Fortune 500-Status erlangt, steigen die Risiken exponentiell an. Im gleichen Maße wie sich Umsatz, Geschäftsprozesse, Anzahl der Mitarbeiter und IT-Ressourcen anhäufen, wachsen und verschmelzen die Risiken. Bei IT-Ressourcen, die zum Generieren von Umsatz dienen, besteht die konkrete Gefahr, dass dieser Umsatzstrom im Falle eines Ausfalls zum Erliegen kommt. Jeder Moment Ausfallzeit führt zu Verlusten. Ebenso wächst mit der Datenmenge das Risiko, dass Kunden geschädigt werden.

In der traditionellen lokalen Welt konzentrieren sich die IT-Governanceteams auf die Bewertung von Risiken, die Erstellung von Prozessen zum Verwalten dieser Risiken und das Bereitstellen von Systemen, um sicherzustellen, dass Abhilfemaßnahmen erfolgreich implementiert werden. Diese Maßnahmen gleichen die Risiken aus, die für den Betrieb in einer verbundenen, modernen Geschäftsumgebung unvermeidbar sind.

## <a name="understand-business-risks-in-the-cloud"></a>Grundlegendes zu Geschäftsrisiken in der Cloud

Während einer Transformation sind dieselben relativen Risiken vorhanden.

- In der frühen Experimentierphase werden einige Ressourcen mit wenigen oder gar keinen relevanten Daten bereitgestellt. Das Risiko ist gering.
- Wenn die erste Workload bereitgestellt wird, steigt das Risiko ein wenig an. Dieses Risiko kann einfach verringert werden, indem Sie eine Anwendung mit von Natur aus geringem Risiko und einer geringen Benutzeranzahl auswählen.
- Während weitere Workloads online geschaltet werden, ändern sich die Risiken mit jedem neuen Release. Neue Apps werden live geschaltet, und Risiken verändern sich.
- Wenn ein Unternehmen die ersten 10 oder 20 Anwendungen online schaltet, liegt ein wesentlich anderes Risikoprofil vor, als wenn die tausendste Anwendung in die Produktion in der Cloud wechselt.

Die Ressourcen, die sich in der herkömmlichen lokalen Umgebung angesammelt haben, haben sich wahrscheinlich im Laufe der Zeit angehäuft. Das Unternehmen und das IT-Team reiften wahrscheinlich in ähnlicher Weise. Dieses parallele Wachstum bringt häufig einige unnötige Richtlinien mit sich.

Während einer Cloudtransformation haben sowohl das Unternehmen als auch das IT-Team die Möglichkeit, diese Richtlinien zurückzusetzen und mit der gewachsenen Erfahrung neue zu erstellen.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-business-risk-mvp"></a>Was ist ein Geschäftsrisiko-MVP?

**Minimum Viable Product (MVP)** ist ein gängiger Ausdruck, um die kleinste Einheit einer Ressource zu definieren, die einen spürbaren Wert erzeugen kann. Bei einem Geschäftsrisiko-MVP geht das Cloudgovernanceteam zunächst davon aus, dass einige Ressourcen irgendwann in einer Cloudumgebung bereitgestellt werden. Es ist zu diesem Zeitpunkt nicht bekannt, was diese Ressourcen sind, und das Team kann sich nicht sicher sein, welche Arten von Daten für diese Ressourcen gespeichert werden.

Beim Planen des Geschäftsrisikos kann das Cloudgovernanceteam für den ungünstigsten Fall vorsorgen und der Cloud jede erdenkliche Richtlinie zuordnen. Die Identifizierung aller potenziellen Geschäftsrisiken für alle Cloudnutzungsszenarien kann erheblichen Zeit- und Arbeitsaufwand erfordern, was die Implementierung von Governance für Ihre Cloudworkloads verzögern kann. Dies ist nicht empfehlenswert, aber es ist eine Option.

Im Gegensatz dazu kann ein MVP-Ansatz es dem Team ermöglichen, einen anfänglichen Ausgangspunkt und eine Reihe von Annahmen zu definieren, die für die meisten/alle Ressourcen gelten würden. Dieses Geschäftsrisiko-MVP unterstützt anfängliche Implementierungen in kleinem Maßstab oder Testcloudbereitstellungen und dient dann als Grundlage für die schrittweise Identifizierung und Behebung neuer Risiken, wenn Geschäftsanforderungen entstehen oder zusätzliche Workloads in Ihre Cloudumgebung aufgenommen werden. Dieser Prozess ermöglicht es Ihnen, Governance während des gesamten Cloudübernahmeprozesses anzuwenden.

Nachfolgend sind einige grundlegende Beispiele für Geschäftsrisiken aufgeführt, die im Rahmen eines MVP berücksichtigt werden können:

- Alle Ressourcen könnten gelöscht werden (durch Fehler, Irrtum oder Wartung).
- Alle Ressourcen könnten zu viele Ausgaben generieren.
- Alle Ressourcen könnten durch unsichere Kennwörter oder Einstellungen kompromittiert werden.
- Ressourcen, deren geöffnete Ports über das Internet zugänglich sind, könnten kompromittiert werden.

Die oben aufgeführten Beispiele sollen die MVP-Geschäftsrisiken als Theorie aufstellen. Die tatsächliche Liste ist für jede Umgebung individuell.
Sobald das Geschäftsrisiko-MVP eingerichtet wurde, kann die Umwandlung in [Richtlinien](./index.md) erfolgen, um die einzelnen Risiken zu mindern.

<!-- markdownlint-enable MD026 -->

## <a name="incremental-risk-mitigation"></a>Inkrementelle Risikominderung

Wenn Ihr Unternehmen immer mehr Workloads in der Cloud bereitstellt, werden die Entwicklungsteams die zunehmenden Cloudressourcen nutzen. Bei jeder Iteration werden neue Ressourcen erstellt und gestaffelt bereitgestellt. Mit jedem Release werden die Workloads für die Höherstufung in die Produktion vorbereitet. Jeder dieser Zyklen besitzt das Potenzial, zuvor nicht erkannte Geschäftsrisiken einzuführen.

Unter der Annahme, dass ein Geschäftsrisiko-MVP der Ausgangspunkt für Ihre ersten Bemühungen zur Einführung der Cloud ist, kann die Governance parallel zu Ihrem zunehmenden Einsatz von Cloudressourcen ausreifen. Wenn das Cloudgovernanceteam parallel zu den Cloudeinführungsteams arbeitet, kann das Wachstum der Geschäftsrisiken bei ihrer Identifizierung angegangen werden, was ein stabiles, kontinuierliches Modell für die Entwicklung der Governancereife bietet.

Jede bereitgestellte Ressource kann ganz einfach nach Risiko klassifiziert werden. Dokumente zur Datenklassifizierung können parallel zu Stagingzyklen erstellt werden. Risikoprofil und Angriffspunkte können ebenso dokumentiert werden. Im Lauf der Zeit besitzt die gesamte Organisation eine sehr klare Übersicht über die Geschäftsrisiken.

Bei jeder Iteration kann das Cloudgovernanceteam mit dem Cloudstrategieteam zusammenarbeiten, um neue Risiken, Minderungsstrategien, Kompromisse und potenzielle Kosten schnell zu kommunizieren. So können Unternehmensbeteiligte und IT-Experten zusammen ausgereifte, fundierte Entscheidungen treffen. Diese Entscheidungen fließen dann in die Richtlinienentwicklung ein. Bei Bedarf rufen die Richtlinienänderungen neue Arbeitselemente für die Entwicklung wichtiger Infrastruktursysteme hervor. Wenn Änderungen an bereitgestellten Systemen erforderlich sind, haben Cloudeinführungsteams genügend Zeit für Änderungen, während das Unternehmen die bereitgestellten Systeme testet und einen Einführungsplan für Benutzer entwickelt.

Dieser Ansatz reduziert Risiken auf ein Mindestmaß und ermöglicht dem Team gleichzeitig eine schnelle Weiterentwicklung. Darüber hinaus stellt er sicher, dass Risiken sofort behandelt und vor der Bereitstellung behoben werden.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie die Risikotoleranz während der Cloudeinführung evaluieren.

> [!div class="nextstepaction"]
> [Evaluieren der Risikotoleranz](./risk-tolerance.md)
