---
title: Finanzmodell für die Cloudmigration
description: Es wird beschrieben, was Sie für die Erstellung eines Finanzmodells benötigen, mit dem der gesamte Geschäftswert einer Cloudtransformation präzise dargestellt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 5280611c88caa3aa2ebb70f615eae8e7b5ff73e4
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94994444"
---
# <a name="create-a-financial-model-for-cloud-transformation"></a>Erstellen eines Finanzmodells für die Cloudtransformation

Die Erstellung eines Finanzmodells, mit dem der gesamte Geschäftswert einer Cloudtransformation präzise dargestellt wird, kann kompliziert sein. Finanzmodelle und geschäftliche Begründungen unterscheiden sich meist für verschiedene Organisationen. In diesem Artikel sind einige Formeln enthalten, und es wird auf einige Punkte hingewiesen, die häufig vergessen werden, wenn Strategen Finanzmodelle erstellen.

## <a name="return-on-investment"></a>Rendite

Die Rendite (Return on Investment, ROI) ist für die Führungs- bzw. Vorstandsebene häufig ein wichtiges Kriterium. Der ROI-Wert wird verwendet, um unterschiedliche Möglichkeiten in Bezug auf die Investition von begrenztem Kapital zu vergleichen. Die ROI-Formel ist recht einfach. Die Details, die zum Ermitteln der einzelnen Eingabewerte für die Formel benötigt werden, sind dagegen möglicherweise nicht ganz so einfach zu erlangen. Die Rendite ist im Wesentlichen der Ertrag, der sich aus einer Erstinvestition ergibt. Der Wert wird normalerweise als Prozentsatz dargestellt:

![Return on Investment (ROI) = (Investitionsertrag - Investitionskosten) / Investitionskosten](../_images/strategy/formula-roi.png)

In den nächsten Abschnitten werden die Daten beschrieben, die Sie zum Berechnen der Erstinvestition und des Investitionsertrags (Einnahmen) benötigen.

## <a name="calculate-initial-investment"></a>Berechnen der Erstinvestition

Die Erstinvestition umfasst die Investitionskosten und Betriebskosten, die für die Durchführung einer Transformation erforderlich sind. Die Klassifizierung der Kosten kann je nach Buchhaltungsmodell und Präferenz des CFO variieren. Diese Kategorie würde Elemente enthalten, wie zu transformierende Dienstleistungen, Softwarelizenzen, die ausschließlich während der Transformation genutzt werden, die Kosten der Clouddienste während der Transformation und ggf. die Kosten für Mitarbeitergehälter während der Transformation.

Addieren Sie diese Kosten, um eine Schätzung der Erstinvestition zu erhalten.

## <a name="calculate-the-gain-from-investment"></a>Berechnen des Investitionsertrags

Zum Berechnen des Investitionsertrags wird häufig noch eine zweite Formel benötigt, die von den Geschäftsergebnissen und den damit verbundenen technischen Änderungen abhängt. Das Berechnen der Einnahmen ist schwieriger als das Berechnen von Kosteneinsparungen.

Für die Berechnung der Einnahmen benötigen Sie zwei Variablen:

![Investitionsertrag = Umsatzdeltawerte + Kostendeltawerte](../_images/strategy/formula-gain-from-investment.png)

Diese Variablen werden in den folgenden Abschnitten beschrieben.

## <a name="revenue-deltas"></a>Umsatzdeltawerte

Umsatzdeltawerte sollten in Zusammenarbeit mit Projektbeteiligten des Unternehmens prognostiziert werden. Nachdem sich die Projektbeteiligten des Unternehmens auf die Auswirkungen auf den Umsatz geeinigt haben, kann diese Information zur Verbesserung der Einnahmenposition verwendet werden.

## <a name="cost-deltas"></a>Kostendeltawerte

Kostendeltawerte umfassen die Erhöhung bzw. Verringerung, die sich aus der Transformation ergibt. Unabhängige Variablen können Kostendeltawerte beeinflussen. Die Einnahmen basieren größtenteils auf harten Kostenfaktoren wie Investitionskostenreduzierung, Kostenvermeidung, Betriebskostenreduzierung und Abschreibungskostenreduzierung. In den folgenden Abschnitten werden einige zu berücksichtigende Kostendeltawerte beschrieben.

### <a name="depreciation-reduction-or-acceleration"></a>Reduzierung oder Beschleunigung von Abschreibungen

Informationen zu Abschreibungen erhalten Sie bei Ihrem CFO bzw. von Ihrer Finanzabteilung. Hier sind zum Thema Abschreibungen nur einige allgemeine Informationen angegeben.

Wenn beim Erwerb einer Ressource Kapital investiert wird, kann diese Investition für finanzielle oder steuerliche Zwecke genutzt werden, um sich für die zu erwartende Lebensdauer der Ressource Vorteile zu verschaffen. Einige Unternehmen betrachten Abschreibungen als Steuervorteil. Andere sehen sie als zwingende, ständige Ausgaben an, die anderen wiederkehrenden Ausgaben im IT-Jahresbudget ähneln.

Wenden Sie sich an Ihre Finanzabteilung, um zu ermitteln, ob ein Verzicht auf Abschreibungen möglich ist und sich dadurch eine positive Auswirkung auf das Kostendelta ergibt.

### <a name="physical-asset-recovery"></a>Kostendeckung für physische Ressourcen

In einigen Fällen können ausgesonderte Ressourcen verkauft werden, um Umsatz zu generieren. Dieser Umsatz wird der Einfachheit halber oft der Kostenreduzierung zugeordnet. Es handelt sich aber eigentlich um eine Steigerung des Umsatzes, die unter Umständen entsprechend besteuert wird. Wenden Sie sich an Ihre Finanzabteilung, um Informationen zu erhalten, ob diese Option geeignet ist und wie der daraus erzielte Umsatz angegeben werden muss.

### <a name="operational-cost-reductions"></a>Betriebskostenreduzierung

Wiederkehrende Ausgaben, die für den Betrieb eines Unternehmens anfallen, werden häufig als Betriebskosten bezeichnet. Dies ist eine breite Kategorie aus. In den meisten Buchhaltungsmodellen umfassen diese Kosten Folgendes:

- Softwarelizenzierung.
- Hostingausgaben.
- Stromrechnungen.
- Mieten für Immobilien.
- Kühlungskosten.
- Temporäre Mitarbeiter für den Betrieb.
- Gerätemieten.
- Ersatzteile.
- Wartungsverträge.
- Reparaturdienstleistungen.
- Dienste für Geschäftskontinuität und Notfallwiederherstellung (BCDR, Business Continuity und Disaster Recovery).
- Andere Kosten, für die keine Investitionsgenehmigungen erforderlich sind.

Diese Kategorie bietet eine der höchsten Einnahmendeltawerte. Wenn Sie eine Cloudmigration in Erwägung ziehen, ist die Zeit, die in die Erstellung einer vollständigen Liste investiert wird, selten verschwendet. Stellen Sie dem CIO und der Finanzabteilung entsprechende Fragen, um sicherzustellen, dass alle Betriebskosten berücksichtigt werden.

### <a name="cost-avoidance"></a>Kostenvermeidung

Wenn Betriebskosten zu erwarten, aber noch nicht Teil eines genehmigten Budgets sind, können sie unter Umständen noch nicht einer Kostenreduzierungskategorie zugeordnet werden. Falls beispielsweise VMware- und Microsoft-Lizenzen im nächsten Jahr neu ausgehandelt und bezahlt werden müssen, handelt es sich noch nicht um vollständig relevante Kosten. Reduzierungen dieser zu erwartenden Kosten werden in Bezug auf die Berechnung von Kostendeltawerten dann wie Betriebskosten behandelt. Auf nicht formaler Ebene sollten sie aber als „Kostenvermeidung“ bezeichnet werden, bis die Aushandlung erfolgt ist und das Budget genehmigt wurde.

### <a name="soft-cost-reductions"></a>Reduzierungen von weichen Kosten

In einigen Unternehmen können auch weiche Kosten in den Kostendeltawerten enthalten sein, z.B. Reduzierung der betrieblichen Komplexität oder Reduzierung der Anzahl von Vollzeitmitarbeitern, die für den Betrieb eines Datencenters benötigt werden. Die Einbeziehung von weichen Kosten ist aber nicht immer ratsam. Mit der Einbeziehung von weichen Kosten wird die nicht dokumentierte Annahme getroffen, dass die Kostenreduzierung auch zu greifbaren Kosteneinsparungen führt. Bei Technologieprojekten kommt es aber nur selten zur Deckung von weichen Kosten.

### <a name="headcount-reductions"></a>Reduzierung der Mitarbeiterzahl

Zeiteinsparungen beim Personal werden häufig der Reduzierung von weichen Kosten zugerechnet. Wenn diese Zeiteinsparungen zu einer tatsächlichen Reduzierung von IT-Gehältern oder -Personal führen, könnten die separat als Reduzierungen der Mitarbeiterzahl angerechnet werden.

Die lokal benötigten Fähigkeiten sind im Allgemeinen aber in ähnlichem (oder höherem) Maße auch in der Cloud erforderlich. Daher wird nach einer Cloudmigration nicht notwendigerweise Personal abgebaut.

Eine Ausnahme zu dieser Regel tritt ein, wenn für den Betrieb erforderliche Dienste von einem Drittanbieter oder Anbieter von verwalteten Diensten (Managed Services Provider, MSP) bereitgestellt werden. Wenn IT-Systeme von einem Drittanbieter verwaltet werden, können die Betriebskosten durch eine cloudnative Lösung oder einen cloudnativen MSP ersetzt werden. Ein cloudnativer MSP arbeitet wahrscheinlich effizienter und unter Umständen auch kostengünstiger. Wenn dies der Fall ist, sind Betriebskostenreduzierungen den harten Kosten zuzuordnen.

### <a name="capital-expense-reductions-or-avoidance"></a>Investitionskostenreduzierung oder -vermeidung

Investitionskosten unterscheiden sich leicht von den Betriebskosten. In dieser Kategorie geht es normalerweise um Aktualisierungszyklen oder Datencentererweiterungen. Ein Beispiel für die Erweiterung eines Datencenters ist ein neuer Hochleistungscluster zum Hosten einer Big Data-Lösung oder eines Data Warehouse. Diese Kosten gehören im Allgemeinen zur Kategorie „Investitionskosten“. Üblicher sind die grundlegenden Aktualisierungszyklen. Einige Unternehmen verfügen über starre Hardwareaktualisierungszyklen, bei denen Ressourcen nach einem regelmäßigen Zyklus ausgesondert und ausgetauscht werden (normalerweise alle drei, fünf oder acht Jahre). Diese Zyklen stimmen oft mit Leasezyklen für Ressourcen oder der prognostizierten Lebensdauer von Ausrüstung überein. Wenn ein Aktualisierungszyklus ansteht, fallen in der IT-Abteilung Investitionskosten zur Beschaffung neuer Ausrüstung an.

Falls ein Aktualisierungszyklus genehmigt und mit einem Budget versehen wurde, kann eine Cloudtransformation dazu beitragen, diese Kosten zu beseitigen. Wenn ein Aktualisierungszyklus geplant wurde, aber die Genehmigung noch nicht erteilt wurde, kann die Cloudtransformation Investitionskosten vermeiden. Beide Reduzierungen fließen in den Kostendeltawert ein.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu [Cloudabrechnungsmodellen](./cloud-accounting.md).

> [!div class="nextstepaction"]
> [Cloudabrechnung](./cloud-accounting.md)
