---
title: Beispiele für Finanzergebnisse
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Finanzergebnissen in Bezug auf die Cloudtransformation vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: e5a01fcc2c0afb7e61e08f60b8330ec7ebb2861f
ms.sourcegitcommit: 4e12d2417f646c72abf9fa7959faebc3abee99d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90776294"
---
# <a name="examples-of-fiscal-outcomes"></a>Beispiele für Finanzergebnisse

Auf der obersten Ebene stehen drei grundlegende Konzepte im Mittelpunkt von Gesprächen über Finanzergebnisse:

- **Umsatz:** Fließt durch den Verkauf von Waren oder Dienstleistungen mehr Geld in das Unternehmen?
- **Kosten:** Muss weniger Geld für die Erzeugung bzw. Erstellung, das Marketing, den Vertrieb oder die Bereitstellung von Waren oder Dienstleistungen ausgegeben werden.
- **Gewinn:** Obwohl sie selten vorkommen, können einige Transformationen sowohl den Umsatz steigern als auch die Kosten senken. Dies ist ein Gewinnergebnis.

Im weiteren Verlauf dieses Artikels werden die oben genannten Finanzergebnisse im Kontext einer Cloudtransformation erläutert.

> [!NOTE]
> Die folgenden Beispiele sind hypothetisch und sollten nicht als Garantie für die mit der Einführung einer Cloudstrategie erzielbaren Erträge betrachtet werden.

## <a name="revenue-outcomes"></a>Umsatzergebnisse

### <a name="new-revenue-streams"></a>Neue Umsatzquellen

Die Cloud bietet die Möglichkeit, neue Produkte für Kunden anzubieten oder vorhandene Produkte auf neue Weise bereitzustellen. Viele Geschäftsleute sehen neue Umsatzquellen als eine innovative, unternehmerische und spannende Chance. Neue Einnahmequellen sind ebenfalls anfällig für Fehler und werden von vielen Unternehmen als hohes Risiko angesehen. Wenn umsatzbezogene Ergebnisse von der IT vorgeschlagen werden, wird es voraussichtlich zu Widerstand kommen. Um diesen Ergebnissen Glaubwürdigkeit zu verleihen, sollten Sie sich mit einem Geschäftsführer zusammentun, der sich bereits als Innovator positioniert hat. Durch die Überprüfung der Umsatzquelle in einer frühen Phase des Prozesses lassen sich Hindernisse von Seiten des Unternehmens vermeiden.

- **Beispiel:** Ein Unternehmen verkauft seit mehr als 100 Jahren Bücher. Ein Mitarbeiter des Unternehmens erkennt, dass die Inhalte auf elektronischem Wege bereitgestellt werden können. Er entwickelt ein Gerät, das den direkten Download der gleichen Bücher ermöglicht und in der Buchhandlung verkauft werden kann. Durch das Gerät werden für Bücher neue Verkäufe in Höhe von _X US_-Dollar erzielt.

### <a name="revenue-increases"></a>Umsatzsteigerungen

Dank globaler Skalierbarkeit und digitaler Reichweite bietet die Cloud Unternehmen die Möglichkeit, den mit bestehenden Umsatzquellen erzielten Umsatz zu steigern. Häufig ist diese Art von Ergebnis auf eine Abstimmung mit der Vertriebs- oder Marketingleitung zurückzuführen.

- **Beispiel:** Ein Unternehmen, das Widgets verkauft, könnte mehr Widgets verkaufen, wenn die Vertriebsmitarbeiter sicher auf den digitalen Katalog und die Lagerbestände des Unternehmens zugreifen könnten. Leider sind diese Daten nur im ERP-System des Unternehmens verfügbar, auf das nur über ein mit dem Netzwerk verbundenes Gerät zugegriffen werden kann. Durch das Erstellen einer mit dem ERP-System verbundenen Dienstfassade und das Verfügbarmachen der Katalogliste und nicht sensiblen Bestandsmengen in einer Anwendung in der Cloud könnten die Vertriebsmitarbeiter vor Ort beim Kunden auf die von ihnen benötigten Daten zugreifen. Die Erweiterung des lokalen Active Directory mit Azure Active Directory (Azure AD) und die Integration des rollenbasierten Zugriffs in die Anwendung würde es dem Unternehmen ermöglichen, den Schutz der Daten sicherzustellen. Dieses einfache Projekt könnte den Umsatz für eine vorhandene Produktlinie um *x %* steigern.

### <a name="profit-increases"></a>Gewinnsteigerungen

Nur selten können mit einem einzigen Projekt gleichzeitig der Umsatz gesteigert und die Kosten gesenkt werden. Wenn dies der Fall ist, sollte die Darstellung eines oder mehrerer Umsatzergebnisse jedoch mit mindestens einem Kostenergebnis abgestimmt werden, um das gewünschte Ergebnis zu kommunizieren.

## <a name="cost-outcomes"></a>Kostenergebnisse

### <a name="cost-reduction"></a>Kostensenkung

Cloud Computing kann die Investitionskosten für Hardware und Software, das Einrichten von Datencentern, den Betrieb von lokalen Datencentern und so weiter senken. Die Kosten für Serverracks, Stromversorgung und Kühlung rund um die Uhr sowie IT-Experten für die Verwaltung der Infrastruktur summieren sich schnell. Durch die Stilllegung eines Datencenters kann die Kapitalbindung reduziert werden. Diese Vorgehensweise wird im Allgemeinen als „Ausstieg aus dem Datencenterbetrieb“ bezeichnet. Die Kostensenkung wird normalerweise an den Mitteln im aktuellen Budget gemessen, das je nach Finanzmanagement des CFO (Chief Financial Officer) ein bis fünf Jahre umfassen kann.

- **Beispiel 1:** Das Datencenter eines Unternehmens verschlingt einen großen Teil des jährlichen IT-Budgets. Die IT entscheidet sich, eine Cloudmigration durchzuführen, und überführt die Ressourcen in diesem Datencenter in IaaS-Lösungen (Infrastructure-as-a-Service), wodurch die Kosten im Laufe der nächsten drei Jahren gesenkt werden.
- **Beispiel 2:** Eine Holdinggesellschaft hat vor Kurzem ein neues Unternehmen erworben. In den Übernahmebedingungen ist festgelegt, dass die neue Entität innerhalb von sechs Monaten aus den aktuellen Datencentern entfernt werden muss. Andernfalls muss die Holdinggesellschaft ein Bußgeld in Höhe von einer Millionen US-Dollar pro Monat zahlen. Das Verschieben der digitalen Ressourcen in die Cloud über eine Cloudmigration könnte eine schnelle Außerbetriebnahme der alten Ressourcen ermöglichen.
- **Beispiel 3:** Ein Unternehmen, das Einkommensteuerberatung für Verbraucher anbietet, verzeichnet 70 Prozent seines Jahresumsatzes in den ersten drei Monaten des Jahrs. Während des restlichen Jahrs bleiben die erheblichen IT-Investitionen des Unternehmens relativ ungenutzt. Eine Cloudmigration könnte es der IT-Abteilung ermöglichen, die erforderliche Compute-/Hostingkapazität für diese drei Monate bereitzustellen. Während der verbleibenden neun Monate könnten die IaaS-Kosten durch Verringern des Computebedarfs erheblich reduziert werden.

<!-- docutune:ignore "Ryan Sorensen" "Director of Application Development and Enterprise Architecture" 1M -->
<!-- cSpell:ignore Coverdell Coverdell's Sorensen -->

### <a name="example-coverdell"></a>Beispiel: Coverdell

Coverdell modernisiert seine Infrastruktur und erzielt mit Azure rekordverdächtige Kosteneinsparungen. Die Entscheidung von Coverdell, in Azure zu investieren und sein Netzwerk aus Websites, Anwendungen, Daten und Infrastruktur in dieser Umgebung zu vereinen, führte zu höheren Kosteneinsparungen, als das Unternehmen jemals erwartet hätte. Durch die Migration zu einer reinen Azure-Umgebung konnten 54.000 US-Dollar an monatlichen Kosten für Co-Location-Dienste eingespart werden. Allein durch die neue, vereinte Infrastruktur des Unternehmens erwartet Coverdell in den nächsten zwei bis drei Jahren Einsparungen von etwa einer Million US-Dollar.

> „Der Zugang zum Azure-Technologiestapel ebnet den Weg für skalierbare, einfach zu implementierende und hoch verfügbare Lösungen, die kostengünstig sind. Dadurch können unsere Architekten die von ihnen bereitgestellten Lösungen deutlich kreativer gestalten.“
>
> Ryan Sorensen
>
> Director of Application Development and Enterprise Architecture
>
> Coverdell

### <a name="cost-avoidance"></a>Kostenvermeidung

Durch die Stilllegung eines Datencenters lassen sich auch zukünftige Aktualisierungszyklen und somit Kosten vermeiden. Der Kauf neuer Hardware und Software, um veraltete lokale Systeme zu ersetzen, wird als Aktualisierungszyklus bezeichnet. In Azure werden die Hardware und das Betriebssystem ohne zusätzliche Kosten für den Kunden regelmäßig gewartet, gepatcht und aktualisiert. Dies versetzt einen CFO in die Lage, geplante zukünftige Ausgaben aus langfristigen finanziellen Prognosen zu streichen. Die Kostenvermeidung wird in Euro gemessen. Sie unterscheidet sich von der Kostensenkung, indem sie grundsätzlich auf ein zukünftiges Budget fokussiert, das noch nicht vollständig genehmigt wurde.

- **Beispiel:** Für das Rechenzentrum eines Unternehmens steht in sechs Monaten eine Verlängerung des Mietvertrags an. Das Datencenter ist seit acht Jahren in Betrieb. Vor vier Jahren hat das Unternehmen mehrere Millionen US-Dollar in die Aktualisierung und Virtualisierung aller Server investiert. Im nächsten Jahr sollen die Hardware und Software erneut aktualisiert werden. Durch Migrieren der Ressourcen in diesem Rechenzentrum im Rahmen einer Cloudmigration könnten Kosten vermieden werden, da die geplante Aktualisierung im prognostizierten Budget des nächsten Jahres wegfallen würde. Zudem könnte sie zu einer Kostensenkung führen, da die Mietkosten verringert oder entfallen würden.

### <a name="capital-expenses-and-operating-expenses"></a>Kapitalkosten und Betriebskosten

Bevor Sie näher auf die Kostenergebnisse eingehen, ist das Verständnis der zwei primären Kostenoptionen wichtig: Kapitalkosten und Betriebskosten.

Mit den folgenden Begriffe werden die Unterschiede zwischen Kapital- und Betriebskosten erläutert, die für Geschäftsgespräche über einen Transformationsprozess wichtig sind.

- **Kapital** sind die finanziellen Mittel und Aktiva eines Unternehmens, die für einen bestimmten Zweck zur Verfügung stehen, z. B. die Erhöhung der Serverkapazität oder die Erstellung einer Anwendung.
- **Kapitalkosten** (Investitionskosten) generieren über einen langen Zeitraum Nutzen. Solche Ausgaben erfolgen in der Regel einmalig und führen zum Erwerb von permanenten Vermögenswerten. Die Kosten für die Erstellung einer Anwendung können als Investitionskosten eingestuft werden.
- **Betriebskosten** sind laufende Kosten für die Geschäftstätigkeiten. Die Nutzung von Clouddiensten in einem nutzungsbasierten Bezahlungsmodell kann als Betriebskosten eingestuft werden.
- **Vermögenswerte** sind wirtschaftliche Ressourcen, die zum Generieren von Mehrwert dienen oder genutzt werden. Server, Data Lakes und Anwendungen können als Vermögenswerte eingestuft werden.
- **Abschreibung** ist eine Verringerung des Werts eines Vermögenswerts im Laufe der Zeit. Von größerer Bedeutung für die Überlegungen hinsichtlich Kapitalkosten im Vergleich zu Betriebskosten ist, dass die Abschreibung die Art und Weise angibt, wie die Kosten eines Vermögenswerts über die Zeiträume verteilt werden, in denen er genutzt wird. Wenn Sie beispielsweise in diesem Jahr eine Anwendung erstellen, deren erwartete durchschnittliche Lebensdauer jedoch fünf Jahre beträgt (wie bei den meisten kommerziellen Anwendungen), werden die Kosten für das Entwicklungsteam und die Tools zum Entwickeln und Bereitstellen der Codebasis gleichmäßig über fünf Jahre abgeschrieben.
- **Bewertung** ist der Prozess, durch den der Wert eines Unternehmens geschätzt wird. In den meisten Branchen beruht die Bewertung auf der Fähigkeit des Unternehmens, unter Berücksichtigung der erforderlichen Betriebskosten für die Herstellung der entsprechenden Waren Umsatz und Gewinn zu generieren. In manchen Branchen – wie etwa dem Einzelhandel – oder bei Transaktionstypen wie Private Equity können Vermögenswerte und Abschreibung bei der Bewertung des Unternehmens eine wichtige Rolle spielen.

Fast immer ist davon auszugehen, dass verschiedene Führungskräfte – einschließlich des CIO (Chief Information Officer) – darüber debattieren, wie das Kapital optimal genutzt werden sollte, um das Unternehmen in der gewünschten Richtung voranzubringen. Dem CIO ein Mittel an die Hand zu geben, umstrittene Kapitalkostengespräche in klare Zurechenbarkeit für Betriebskosten umzuwandeln, könnte an sich schon ein attraktives Ergebnis sein. In vielen Branchen suchen CFOs aktiv nach Möglichkeiten zur besseren Zuordnung der finanziellen Verantwortlichkeit zu den Kosten der verkauften Waren.

Bevor Sie jedoch einen Transformationsvorschlag mit dieser Art von Überlegungen zu Kapital- im Vergleich zu Betriebskosten verbinden, ist es ratsam, sich mit Mitgliedern des CFO- oder CIO-Teams zu treffen, um festzustellen, welche Kostenstruktur das Unternehmen bevorzugt. In einigen Unternehmen ist die Verringerung von Kapitalkosten zugunsten von Betriebskosten ein höchst unerwünschtes Ergebnis. Wie zuvor erwähnt, ist dieser Ansatz mitunter bei Einzelhandels-, Holding- und Private Equity-Unternehmen der Fall, die viel Wert auf herkömmliche Anlagenrechnungsmodelle, aber wenig Wert auf intellektuelles Eigentum legen. Auch bei Unternehmen, die in der Vergangenheit negative Erfahrungen mit der Auslagerung von IT-Mitarbeitern oder anderen Funktionen gemacht haben, ist dies zu beobachten.

Ist ein Betriebskostenmodell gewünscht, kann das folgende Beispiel ein tragfähiges Geschäftsergebnis sein:

- **Beispiel:** Das Rechenzentrum eines Unternehmens wird derzeit jährlich mit _x US-Dollar_ für die nächsten drei Jahre abgeschrieben. Im nächsten Jahr wird für eine Aktualisierung der Hardware ein zusätzlicher Kostenaufwand von _y US-Dollar_ erwartet. Wir können die Kapitalkosten in ein Betriebskostenmodell mit einer gleichmäßigen Rate von _z US-Dollar_ pro Monat umwandeln, wodurch eine bessere Verwaltung und Zurechenbarkeit der Betriebskosten für die Technologie möglich wird.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu [Agilitätsergebnissen](./agility-outcomes.md).

> [!div class="nextstepaction"]
> [Agilitätsergebnisse](./agility-outcomes.md)
