---
title: Auf Migration ausgerichtete Kostenkontrollmechanismen
description: Es wird beschrieben, wie Sie Budgets und Zahlungen einrichten und was bei Rechnungen für Ihre Azure-Ressourcen zu beachten ist.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 8486d4de8b6055d6d0741d008c10a405c27b8f92
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803516"
---
# <a name="migration-focused-cost-control-mechanisms"></a>Auf Migration ausgerichtete Kostenkontrollmechanismen

Die Cloud bewirkt einige Veränderungen in unseren Arbeitsweisen, unabhängig von unserer Rolle im Technologieteam. Kosten sind ein gutes Beispiel hierfür. In der Vergangenheit beschäftigte sich nur die Finanz- und IT-Führung mit den Kosten von IT-Ressourcen (Infrastruktur, Apps, Daten). Die Cloud befähigt nun jedes IT-Mitglied, Entscheidungen zu treffen und umzusetzen, die den Endbenutzer besser unterstützen. Mit dieser Fähigkeit kommt jedoch auch die Verantwortung, bei diesen Entscheidungen kostenbewusst zu handeln.

In diesem Artikel werden die Tools vorgestellt, die helfen können, vor, während und nach einer Migration zu Azure sinnvolle Kostenentscheidungen zu treffen.

In diesem Artikel werden folgende Tool behandelt:

> - Azure Migrate
> - Azure-Preisrechner
> - Azure-Gesamtkostenrechner
> - Azure Cost Management
> - Azure Advisor

Die in diesem Artikel beschriebenen Prozesse können auch eine Partnerschaft mit IT-Managern, Finanzexperten oder Branchenanwendungen erfordern.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migrationtabestimatevmcosts"></a>[Schätzen der Kosten für virtuelle Computer vor der Migration](#tab/EstimateVMCosts)

Vor der Migration von Ressourcen (Infrastruktur, Apps oder Daten), besteht die Möglichkeit, die Kosten zu schätzen und die Größe basierend auf beobachteten Leistungskriterien für diese Ressourcen zu optimieren. Die Kostenschätzung dient zwei Zwecken: Sie ermöglicht die Kostenkontrolle und stellt einen Prüfpunkt dar, um sicherzustellen, dass die notwendigen Leistungsanforderungen in den aktuellen Budgets berücksichtigt werden.

## <a name="cost-calculators"></a>Kostenrechner

Für manuelle Kostenberechnungen gibt es zwei praktische Rechner, die eine schnelle Kostenschätzung basierend auf der Architektur der zu migrierenden Workload liefern können.

- Der Azure-[Preisrechner](https://azure.microsoft.com/pricing/calculator) liefert Kostenschätzungen basierend auf manuell eingegebenen Azure-Produkten.
- Manchmal erfordern Entscheidungen einen Vergleich der zukünftigen Cloudkosten mit den aktuellen Kosten der lokalen Architektur. Der [Gesamtkostenrechner](https://azure.microsoft.com/pricing/tco/calculator) kann einen solchen Vergleich liefern.

Diese manuellen Kostenrechner können einzeln verwendet werden, um potenzielle Ausgaben und Einsparungen vorherzusagen. Sie können auch in Verbindung mit den Kostenprognosetools von Azure Migrate verwendet werden, um die Kostenerwartungen an alternative Architekturen oder Leistungsbeschränkungen anzupassen.

## <a name="azure-migrate-calculations"></a>Azure Migrate-Berechnungen

**Voraussetzungen:** Beim Rest dieser Registerkarte wird davon ausgegangen, dass der Leser Azure Migrate bereits mit einer Sammlung von zu migrierenden Ressourcen (Infrastruktur, Apps und Daten) gefüllt hat. Der vorherige Artikel über Bewertungen enthält Anweisungen zum Sammeln der Ausgangsdaten. Sobald die Daten gefüllt wurden, führen Sie die nächsten Schritte aus, um die monatlichen Kosten basierend auf den gesammelten Daten zu schätzen.

Azure Migrate berechnet **monatliche Kostenschätzungen** basierend auf Daten, die vom Collector und der Dienstzuordnung erfasst wurden. Mit den folgenden Schritten werden die Kostenschätzungen geladen:

1. Navigieren Sie im Portal zu „Azure Migrate-Bewertung“.
2. Wählen Sie auf der Seite **Übersicht** des Projekts die Option **+ Bewertung erstellen** aus.
3. Klicken Sie auf **Alle anzeigen**, um die Eigenschaften für die Bewertung zu überprüfen.
4. Erstellen Sie die Gruppe, und geben Sie einen Gruppennamen an.
5. Wählen Sie die Computer aus, die der Gruppe hinzugefügt werden sollen.
6. Klicken Sie auf **Bewertung erstellen**, um die Gruppe und die Bewertung zu erstellen.
7. Zeigen Sie die Bewertung nach der Erstellung in „Übersicht“ > „Dashboard“ an.
8. Wählen Sie im Abschnitt „Bewertungsdetails“ der Portalnavigation die Option **Kostendetails** aus.

Die unten abgebildete resultierende Schätzung identifiziert die monatlichen Kosten für Computing und Speicherung, die oft den größten Teil der Cloudkosten ausmachen.

![Ansicht „Kostendetails“](./media/manage-costs/compute-storage-monthly-cost-estimate.png)
*Abbildung 1 der Ansicht „Kostendetails“ einer Bewertung in Azure Migrate.*

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Einrichten und Überprüfen einer Bewertung mit Azure Migrate](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- Einen umfassenderen Plan zur Kostenverwaltung für eine größere Anzahl von Ressourcen (Infrastruktur, Apps und Daten) bietet das [Governancemodell für das Framework für die Cloudeinführung (Cloud Adoption Framework)](../../govern/guides/index.md). Hierzu gehören insbesondere die Hinweise zur [Disziplin „Kostenverwaltung“](../../govern/cost-management/index.md) und der [Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Cost Management](../../govern/guides/complex/cost-management-improvement.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migrationtabestimateoptimize"></a>[Schätzen und Optimieren der VM-Kosten während und nach der Migration](#tab/EstimateOptimize)

Eine Kostenschätzung vor der Migration bietet ein solides Ziel für die Kostenerwartungen. Sie bietet zudem die Möglichkeit, den Leistungs- und Kostenbedarf jeder zu migrierenden Ressource (Infrastruktur, Apps und Daten) zu berücksichtigen. Es handelt sich jedoch immer noch um eine Schätzung. Sobald die Ressource migriert wurde und unter Last steht, können genauere Kostenberechnungen auf der Grundlage der tatsächlichen oder synthetisierten Last durchgeführt werden.

## <a name="azure-advisor-cost-recommendations"></a>Azure Advisor-Empfehlungen zu Kosten

Innerhalb von 24 Stunden nach der Migration von Ressourcen (Infrastruktur, Apps und Daten) zu Azure beginnt Azure Advisor mit der Überwachung der Leistung jeder Ressource, um Ihnen Feedback zur Ressource zu geben. Ein erfasstes Feedbackelement bezieht sich auf die Ausgewogenheit zwischen Kosten und Auslastung.

Die folgenden Schritte stellen Kostenempfehlungen für Ressourcen (Infrastruktur, Apps und Daten) innerhalb Ihrer aktuellen Abonnements bereit:

1. Navigieren Sie im Portal zu **Azure Advisor**. Wählen Sie dazu im linken Navigationsbereich des Azure-Portals **Advisor** aus. Wird „Advisor“ im linken Bereich nicht angezeigt, wählen Sie **Alle Dienste** aus. Wählen Sie im Dienstmenübereich unter **Überwachung und Verwaltung** die Option **Advisor** aus.
2. Das Advisor-Dashboard zeigt eine Zusammenfassung Ihrer Empfehlungen für alle ausgewählten Abonnements an. Sie können mithilfe der Abonnementfilter-Dropdownliste die Abonnements auswählen, für die Empfehlungen angezeigt werden sollen.
3. Um Empfehlungen zu Kosten anzuzeigen, wählen Sie die Registerkarte „Kosten“ aus.

## <a name="azure-cost-management"></a>Azure Cost Management

Azure Cost Management bietet eine ganzheitlichere Sicht auf die Ausgabengewohnheiten, einschließlich einer detaillierten Sicht auf Kosten- und Ausgabentrends im Zeitverlauf. Bei großen oder komplexen Migrationen kann diese Sicht die notwendigen Erkenntnisse liefern, um umfassende, weitreichende Kostenverwaltungsentscheidungen zu treffen.

Voraussetzungen: Beim Rest dieser Registerkarte wird davon ausgegangen, dass der Leser das Setup von Azure Cost Management während der Fertigstellung des Leitfadens für die Azure-Einrichtung abgeschlossen hat. Weitere Details zur Konfiguration von Azure Cost Management finden Sie in [diesem Artikel des Leitfadens für die Azure-Einrichtung](../../ready/azure-setup-guide/manage-costs.md). Sobald die Daten gefüllt wurden, führen Sie die nächsten Schritte aus, um die monatlichen Kosten basierend auf den gesammelten Daten zu schätzen.

Mit den folgenden Schritten werden die Azure Cost Management-Kostenanalysedaten für Ihre Abonnements geladen:

1. Navigieren Sie im Portal zu **Cost Management + Abrechnung**. Wird „Kostenverwaltung + Abrechnung“ im linken Bereich nicht angezeigt, klicken Sie auf **Alle Dienste**. Klicken Sie im Dienstmenübereich unter **Überwachung und Verwaltung** auf **Kostenverwaltung + Abrechnung**.
2. Wählen Sie auf dem Blatt „Cost Management + Abrechnung“ im linken Navigationsbereich die Option **Kostenverwaltung** aus, um mit der Analyse und Optimierung der Cloudkosten zu beginnen.
3. Wählen Sie auf dem Blatt „Cost Management“ die Option **Kostenanalyse** aus.
    a. Verwenden Sie **Bereich**, um in einen anderen Bereich der Kostenanalyse zu wechseln.

Anhand dieser Analyse können Sie die Gesamtkosten, das Budget (falls vorhanden) und die kumulierten Kosten überprüfen. Jede Berechnung kann nach Dienst, nach Ressource und im Zeitverlauf angezeigt werden. Und was am Wichtigsten ist: Die Kosten können nach Tags analysiert werden. Korrekte Namen und ein ordnungsgemäßes Tagging von Ressourcen (Infrastruktur, Apps und Daten) stellen den grundlegenden Ausgangspunkt für solide Governance- und Kostenverwaltungsprozesse dar. Geeignete Tags ermöglichen eine bessere Kostenverwaltung und deutlicheren Einfluss auf Leistungs- und Kostenoptimierungen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- Einen umfassenderen Plan zur Kostenverwaltung für eine größere Anzahl von Ressourcen (Infrastruktur, Apps und Daten) bietet das [Governancemodell für das Framework für die Cloudeinführung (Cloud Adoption Framework)](../../govern/guides/index.md). Hierzu gehören insbesondere die Hinweise zur [Disziplin „Kostenverwaltung“](../../govern/cost-management/index.md) und der [Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Cost Management“](../../govern/guides/complex/cost-management-improvement.md).
- Weitere Informationen zu Azure Advisor finden Sie unter [Reduzieren der Dienstkosten mit Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations).
- Weitere Informationen zu Azure Cost Management finden Sie unter [Verstehen von und Arbeiten mit Bereichen](https://docs.microsoft.com/azure/cost-management/understand-work-scopes) und [Ermitteln und Analysieren von Kosten mit der Kostenanalyse](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis).

# <a name="tips-and-tricks-to-optimize-coststabtipstricks"></a>[Tipps und Tricks zur Kostenoptimierung](#tab/TipsTricks)

Zusätzlich zu den in diesem Artikel genannten Tools gibt es einige Tipps und Tricks, die helfen können, die Gesamtcloudkosten schnell zu senken. Im Folgenden finden Sie einige wichtige Tipps, die Sie beachten sollten:

## <a name="avoid-unnecessary-spending"></a>Vermeiden unnötiger Ausgaben

Die meisten Ressourcen (Infrastruktur, Apps und Daten) in einem vorhandenen Datencenter können theoretisch in die Cloud migriert werden. Allerdings bedeutet das nicht, dass dies immer sinnvoll ist. Überprüfen Sie während der Bewertung der einzelnen Workloads, ob die Workload migriert werden sollte. Mithilfe des Artikels im „Framework für die Cloudeinführung (Cloud Adoption Framework)“ über [inkrementelle Rationalisierung](../../digital-estate/rationalize.md) können Sie feststellen, welche Assets migriert werden sollten.

## <a name="reduce-waste"></a>Reduzieren der Ressourcenvergeudung

Nachdem Sie Ihre Infrastruktur in Azure bereitgestellt haben, müssen Sie sicherstellen, dass sie tatsächlich genutzt wird. Die einfachste Möglichkeit zum sofortigen Erzielen von Einsparungen besteht darin, Ihre Ressourcen zu überprüfen und alle nicht genutzten Ressourcen zu entfernen.

## <a name="reduce-overprovisioning"></a>Reduzieren der Überbereitstellung

Selbst bei den besten Ansätzen für die Schätzung kann es zu überdimensionierten und nicht ausgelasteten Ressourcen (Infrastruktur, Apps und Daten) kommen. Durch Überprüfung dieser Ressourcen unter Verwendung der Tools in den beiden vorherigen Registerkarten können Sie mögliche Mittel zur Reduzierung der Ressourcengröße identifizieren, um die Leistungsanforderungen besser zu erfüllen und die Kosten zu senken.

## <a name="take-advantage-of-available-discounts"></a>Nutzen Sie verfügbare Rabatte

Sprechen Sie mit Ihrem Microsoft-Kundenbetreuer, um zu verstehen, wie Sie aktuelle Rabattoptionen nutzen können. Im Folgenden finden Sie einige Beispiele für Rabatte, die häufig zur Kostensenkung genutzt werden.

## <a name="azure-reservations"></a>Azure-Reservierungen

Mit [Azure-Reservierungen](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) können Sie Computekapazitäten für Ihre virtuellen Computer oder SQL-Datenbank-Instanzen für ein Jahr oder drei Jahre im Voraus erwerben. Bei der Vorauszahlung können Sie einen Rabatt für die Ressourcen in Anspruch nehmen, die Sie nutzen. Azure-Reservierungen können die Computekosten für Ihre virtuellen Computer oder SQL-Datenbank-Instanzen mit einer Vorauszahlung für ein Jahr oder drei Jahre erheblich reduzieren (um bis zu 72 Prozent im Vergleich zu den Preisen bei nutzungsbasierter Bezahlung). Reservierungen bieten einen Abrechnungsrabatt und wirken sich nicht auf den Laufzeitstatus Ihrer virtuellen Computer oder SQL-Datenbank-Instanzen aus.

## <a name="use-azure-hybrid-benefit"></a>Verwenden des Azure-Hybridvorteils

Wenn in Ihren lokalen Bereitstellungen Windows Server- oder SQL Server-Lizenzen vorhanden sind, können Sie den [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit) nutzen, um in Azure bares Geld zu sparen. Beim Vorteil für Windows Server deckt jede Lizenz die Kosten des Betriebssystems (auf bis zu zwei virtuellen Computern) ab, und Sie zahlen nur die grundlegenden Computekosten. Sie können vorhandene SQL Server-Lizenzen verwenden, um bei auf virtuellen Kernen basierenden SQL-Datenbank-Optionen bis zu 55 Prozent zu sparen. Zu den Optionen gehören SQL Server in Azure Virtual Machines und SQL Server Integration Services.

## <a name="low-priority-vms-with-batch"></a>VMs mit niedriger Priorität mit Batch

Für Hintergrundprozesse mit niedrigerer Priorität stellt Batch eine Möglichkeit zum Verwalten von Hintergrunddienst-VMs und Senken der Kosten dar. Allerdings sollten Sie vor der Auswahl dieser Rabattoption verstehen, welche Auswirkungen [VMs mit niedriger Priorität mit Batch](https://docs.microsoft.com/azure/batch/batch-low-pri-vms) auf die Leistung haben.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Einen umfassenderen Plan zur Kostenverwaltung für eine größere Anzahl von Ressourcen (Infrastruktur, Apps und Daten) bietet das [Governancemodell für das Framework für die Cloudeinführung (Cloud Adoption Framework)](../../govern/guides/index.md). Hierzu gehören insbesondere die Hinweise zur [Disziplin „Kostenverwaltung“](../../govern/cost-management/index.md) und der [Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Cost Management“](../../govern/guides/complex/cost-management-improvement.md).
