---
title: Bewährte Methoden für Kostenermittlung und Größenanpassung von zu Azure migrierten Workloads
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den bewährten Methoden für Kostenermittlung und Größenanpassung von zu Azure migrierten Workloads vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b22f93d4251f03c87ecdeb6dbef8ea932f48476f
ms.sourcegitcommit: 580a6f66a0d0f3f5b755c68d757a84b2351a432f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473249"
---
<!-- docsTest:ignore ARO -->

# <a name="best-practices-to-cost-and-size-workloads-migrated-to-azure"></a>Bewährte Methoden für Kostenermittlung und Größenanpassung von zu Azure migrierten Workloads

Wenn sie sich bei der Planung und dem Entwurf einer Migration auf die Kosten konzentrieren, sichert dies den langfristigen Erfolg Ihrer Azure-Migration. Während eines Migrationsprojekts ist es entscheidend, dass alle Teams (Finanzen, Verwaltung, Teams für die Anwendungsentwicklung) die damit verbundenen Kosten kennen und verstehen.

- Vor der Migration ist es wichtig, dass Sie über eine Baseline für die monatlichen, vierteljährlichen und jährlichen Budgetziele verfügen. So können Sie den Betrag schätzen, den Sie für Ihre Migration ausgeben möchten, und den Erfolg sicherstellen.
- Nach der Migration sollten Sie Kosten optimieren, Workloads kontinuierlich überwachen und bereits für zukünftige Verwendungsmuster planen. Migrierte Ressourcen können eventuell als eine Art von Workload beginnen, sich jedoch im Laufe der Zeit in einen anderen Typ entwickeln, basierend auf Nutzung, Kosten und sich verändernden Geschäftsanforderungen.

In diesem Artikel werden bewährte Methoden für die Vorbereitung und Verwaltung in Bezug auf die Kosten und die Größe vor und nach der Migration beschrieben.

> [!IMPORTANT]
> Die in diesem Artikel wiedergegebenen bewährten Methoden und Meinungen basieren auf Azure-Plattform- und --Dienstfunktionen, die zum Zeitpunkt der Niederschrift verfügbar sind. Features und Funktionen ändern sich im Laufe der Zeit. Nicht alle Empfehlungen sind notwendigerweise auf Ihre Bereitstellung anwendbar. Wählen Sie also aus, was für Sie funktioniert.

## <a name="before-migration"></a>Vor der Migration

Bevor Sie Ihre Workloads in die Cloud verschieben, schätzen Sie die monatlichen Kosten für ihren Betrieb in Azure ab. Die proaktive Verwaltung von Cloudkosten hilft Ihnen dabei, Ihr Budget für Betriebsaufwendungen einzuhalten. Wenn das Budget beschränkt ist, berücksichtigen Sie dies vor der Migration. Erwägen Sie, Workloads in serverlose Azure-Technologien zu konvertieren, falls möglich, um Kosten zu senken.

Die bewährten Methoden in diesem Abschnitt helfen Ihnen bei der Durchführung der folgenden Aufgaben:

- Schätzen der Kosten
- Durchführen der richtigen Größenanpassung für virtuelle Computer (VMs) und Speicher
- Verwenden des Azure-Hybridvorteils
- Verwenden von Azure Reserved Virtual Machine Instances
- Schätzen der übergreifenden Cloudausgaben für Abonnements

## <a name="best-practice-estimate-monthly-workload-costs"></a>Bewährte Methode: Monatliche Workloadkosten abschätzen

Um eine Prognose für Ihre monatliche Rechnung für migrierte Workloads aufzustellen, gibt es eine Reihe von Tools, die Sie verwenden können.

<!-- TODO: Change "input costs" -->

- **Azure-Preisrechner:** Wählen Sie die Produkte aus, für die Sie die Schätzung erstellen möchten, z. B. VMs und Speicher. Geben Sie anschließend die Kosten in den Rechner ein, um eine Schätzung zu erstellen.

  ![Screenshot: Azure-Preisrechner](./media/migrate-best-practices-costs/pricing.png)
    _Abbildung 1: Azure-Preisrechner_

- **Azure Migrate:** Um Kosten zu schätzen, müssen Sie alle Ressourcen überprüfen und berücksichtigen, die für die Ausführung Ihrer Workloads in Azure erforderlich sind. Um diese Daten zu sammeln, erstellen Sie ein Inventar Ihrer Ressourcen, einschließlich Servern, virtueller Computer, Datenbanken und Speicher. Sie können Azure Migrate verwenden, um diese Informationen zu sammeln.

  - Azure Migrate ermittelt und bewertet Ihre lokale Umgebung, um ein Inventar aufzustellen.
  - Azure Migrate kann Abhängigkeiten zwischen VMs zuordnen und anzeigen, damit Sie ein vollständiges Bild erhalten.
  - Eine Azure Migrate-Bewertung enthält geschätzte Kosten.
    - **Computekosten:** Wenn Sie eine Bewertung erstellen, berechnet Azure Migrate anhand der empfohlenen Azure-VM-Größe und mithilfe der Azure-Abrechnungs-APIs die geschätzten monatlichen Kosten für den virtuellen Computer (VM-Kosten). Bei der Schätzung werden Betriebssystem, Software Assurance, Azure Reserved Virtual Machine Instances, VM-Betriebszeit, Standort und Währungseinstellungen berücksichtigt. Die Kosten aller virtuellen Computer werden in der Bewertung zusammengefasst, um so die monatlichen Compute-Gesamtkosten zu berechnen.
    - **Speicherkosten:** Azure Migrate berechnet die monatlichen Speichergesamtkosten durch Aggregieren der Speicherkosten aller virtuellen Computer in einer Bewertung. Sie können die monatlichen Speicherkosten für einen bestimmten Computer berechnen, indem Sie die monatlichen Kosten aller an den Computer angefügten Datenträger zusammenfassen.

    ![Screenshot: Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    _Abbildung 2: Azure Migrate-Bewertung_

**Weitere Informationen**:

- [Verwenden](https://azure.microsoft.com/pricing/calculator) des Azure-Preisrechners.
- Sehen Sie sich die [Übersicht zu Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) an.
- [Lesen von Informationen zu](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) Azure Migrate-Bewertungen.
- Erfahren Sie mehr über [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).

## <a name="best-practice-right-size-vms"></a>Bewährte Methode: Richtige Größe von virtuellen Computern anpassen

Sie können eine Reihe von Optionen auswählen, wenn Sie virtuelle Azure-Computer bereitstellen, um Workloads zu unterstützen. Jeder VM-Typ verfügt über bestimmte Features und verschiedene Kombinationen aus CPU, Arbeitsspeicher und Datenträgern. VMs sind wie in der folgenden Tabelle gruppiert:

| type | Details | Verwendung |
| --- | --- | --- |
| **Allgemeiner Zweck** | Ausgewogenes Verhältnis von CPU zu Arbeitsspeicher. | Gut geeignet für Tests und Entwicklung, kleine bis mittlere Datenbanken und Webserver mit geringer bis mittlerer Auslastung. |
| **Compute-optimiert** | Hohes Verhältnis von CPU zu Arbeitsspeicher. | Gut geeignet für Webserver für mittlere Mengen an Datenverkehr, Netzwerkgeräte, Stapelverarbeitungsvorgänge und Anwendungsserver. |
| **Arbeitsspeicheroptimiert** | Hohes Verhältnis von Speicher zu CPU. | Gut geeignet für relationale Datenbanken, mittlere bis große Caches und In-Memory-Analysen. |
| **Speicheroptimiert** | Datenträgerdurchsatz und E/A-Vorgänge auf hohem Niveau. | Gut geeignet für Big Data sowie SQL- und NoSQL-Datenbanken. |
| **GPU-optimiert** | Spezialisierte VMs. Einzelne oder mehrere GPUs. | Anspruchsvolle Grafik- und Videobearbeitung. |
| **Hohe Leistung** | Schnellste und leistungsfähigste CPU. VMs mit optionalen Netzwerkschnittstellen mit hohem Durchsatz (RDMA). | Kritische Hochleistungsanwendungen. |

- Es ist wichtig, die Preisunterschiede zwischen diesen virtuellen Computern zu verstehen sowie die langfristigen Auswirkungen auf das Budget.
- Jeder Typ umfasst eine bestimmte Anzahl darin enthaltener VM-Serien.
- Außerdem können Sie, wenn Sie eine VM innerhalb einer Serie auswählen, die VM nur innerhalb dieser Serie zentral hoch- oder herunterskalieren. Eine `DS2_v2`-Instanz kann beispielsweise bis zu `DS4_v2` hochskaliert werden, aber sie kann nicht in eine Instanz einer anderen Serie, z. B. eine `F2s_v2`-Instanz, geändert werden.

**Weitere Informationen**:

- Erfahren Sie mehr zu [VM-Typen und -Größenanpassung](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) sowie zur Zuordnung von Größen zu Typen.
- Planen Sie [Größen für VM-Instanzen](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs).
- Arbeiten Sie eine [Beispielbewertung für das fiktive Unternehmen Contoso](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) durch.

## <a name="best-practice-select-the-right-storage"></a>Bewährte Methode: Den richtigen Speicher auswählen

Das Optimieren und Verwalten von lokalem Speicher (SAN oder NAS) sowie der Netzwerke, die diesen unterstützen, können teuer und zeitaufwendig sein. Datei(Speicher)daten werden häufig zur Cloud migriert, um Schwierigkeiten beim Betrieb und der Verwaltung zu beseitigen. Microsoft bietet verschiedene Optionen zum Verschieben von Daten in Azure, und Sie müssen sich hinsichtlich dieser Optionen entscheiden. Die Auswahl des richtigen Speichertyps für Daten kann Ihrer Organisation jeden Monat mehrere tausend Euro sparen. Beachten Sie dabei Folgendes:

- Daten, auf die nur selten zugegriffen wird und die nicht unternehmenskritisch sind, müssen nicht im teuersten Speicher platziert werden.
- Umgekehrt sollten sich unternehmenskritische Daten auf Speicheroptionen eines höheren Tarifs befinden.
- Erstellen Sie während der Migrationsplanung ein Inventar der Daten, und klassifizieren Sie sie nach Wichtigkeit, um sie dem jeweils optimal geeigneten Speicher zuzuordnen. Berücksichtigen Sie hierbei Budget und Kosten sowie die Leistung. Die Kosten sollten nicht unbedingt der entscheidende Faktor sein. Die Entscheidung für die kostengünstigste Option kann unter Umständen dazu führen, dass die Workload Leistungs- und Verfügbarkeitsrisiken ausgesetzt ist.

### <a name="storage-data-types"></a>Speicherdatentypen

Azure bietet verschiedene Arten von Speicherdaten.

| Datentyp | Details | Verwendung |
| --- | --- | --- |
| **Blobs** | Optimiert für die Speicherung großer Mengen von unstrukturierten Objekten wie z. B. Text- oder Binärdaten. <br><br> | Zugriff auf Daten von überall her über HTTP/HTTPS. <br><br> Verwendung für Szenarios mit Streaming und wahlfreiem Zugriff. Beispielsweise um einem Browser Bilder und Dokumente direkt bereitzustellen, Video und Audio zu streamen und Sicherungs- und Notfallwiederherstellungsdaten zu speichern. |
| **Dateien** | Verwaltete Dateifreigaben, auf die über SMB 3.0 zugegriffen wird. | Verwendung beim Migrieren lokaler Dateifreigaben sowie zur Bereitstellung von mehrfachem Zugriff bzw. mehreren Verbindungen, um Daten abzulegen. |
| **Datenträger** | Basierend auf Seitenblobs. <br><br> Datenträgertyp: Standard (HDD oder SSD) oder Premium (SSD). <br><br> Datenträgerverwaltung: Nicht verwaltet (Sie verwalten Datenträgereinstellungen und Speicher) oder verwaltet (Sie wählen den Datenträgertyp aus, und Azure verwaltet diesen Datenträger für Sie). | Verwendung von Premium-Datenträgern für VMs. Verwendung von verwalteten Datenträgern für einfache Verwaltung und Skalierung. |
| **Warteschlangen** | Speichern und Abrufen großer Mengen von Nachrichten mittels Zugriff über authentifizierte Aufrufe (HTTP oder HTTPS). | Verbinden von Anwendungskomponenten mit asynchronem Message Queuing. |
| **Tabellen** | Speichern von Tabellen. | Dieser Datentyp ist Teil der Azure Cosmos DB-Tabellen-API. |

### <a name="access-tiers"></a>Zugriffsebenen

Azure Storage bietet verschiedene Optionen für den Zugriff auf Blockblobdaten. Die Auswahl der richtigen Zugriffsebene hilft sicherzustellen, dass Sie Blockblobdaten auf möglichst kostengünstige Art und Weise speichern.

| Zugriffsebene | Details | Verwendung |
| --- | --- | --- |
| **Heiße Ebene** | Höhere Speicherkosten als kalte Ebene. Niedrigere Zugriffsgebühren als kalte Ebene. <br><br> Dies ist die Standardebene. | Verwendung für Daten, die aktiv und mit häufigem Zugriff verwendet werden. |
| **Kalte Ebene** | Niedrigere Speicherkosten als heiße Ebene. Höhere Zugriffsgebühren als heiße Ebene. <br><br> Speicherung für mindestens 30 Tage. | Kurzfristige Speicherung. Die Daten sind verfügbar, aber es wird nur selten darauf zugegriffen. |
| **Archivieren** | Verwendung für einzelne Blockblobs. <br><br> Kostengünstigste Option für Speicherung. Datenzugriff ist teurer als bei heißer oder kalter Ebene. | Verwendung für Daten, die mehrere Stunden Serverabrufwartezeit tolerieren und mindestens 180 Tage lang auf dieser Ebene verbleiben. |

### <a name="storage-account-types"></a>Speicherkontotypen

Azure bietet verschiedene Typen von Speicherkonten und Leistungsstufen.

| Kontotyp | Details | Verwendung |
| --- | --- | --- |
| **Universell V2 Standard** | Unterstützt Blobs (Block-, Seiten- und Anfügeblobs), Dateien, Datenträger, Warteschlangen und Tabellen. <br><br> Unterstützt die Zugriffsebenen „Heiß“, „Kalt“ und „Archiv“. Zonenredundanter Speicher (ZRS) wird unterstützt. | Verwendung für die meisten Szenarios und die meisten Typen von Daten. Standardspeicherkonten können auf HDDs oder SSDs basieren. |
| **Universell V2 Premium** | Unterstützt die Blobspeicherdaten (Seitenblobs). Unterstützt die Zugriffsebenen „Heiß“, „Kalt“ und „Archiv“. ZRS wird unterstützt. <br><br> Speicherung auf SSDs. | Microsoft empfiehlt die Verwendung für alle VMs. |
| **Universell V1** | Zugriffsebenen werden nicht unterstützt. ZRS wird nicht unterstützt. | Verwendung, wenn Anwendungen das klassische Azure-Bereitstellungsmodell benötigen. |
| **Blob** | Spezialisiertes Speicherkonto zum Speichern unstrukturierter Objekte. Bietet nur Blockblobs und Anfügeblobs (keine Datei-, Warteschlangen-, Tabellen- oder Datenträgerspeicherdienste). Bietet dieselbe Dauerhaftigkeit, Verfügbarkeit, Skalierbarkeit und Leistung wie „Universell V2“. | Sie können in diesen Konten keine Seitenblobs und deshalb auch keine VHD-Dateien speichern. Sie können eine Zugriffsebene auf „Heiß“ oder „Kalt“ festlegen. |

### <a name="storage-redundancy-options"></a>Redundanzoptionen für Storage

Speicherkonten können verschiedene Arten von Redundanz für Resilienz und Hochverfügbarkeit verwenden.

| type | Details | Verwendung |
| --- | --- | --- |
| **Lokal redundanter Speicher (LRS)** | Schützt vor einem lokalen Ausfall durch Replikation in eine einzelne Speichereinheit in einer gesonderten Fehler- und Updatedomäne. Behält mehrere Kopien Ihrer Daten in einem Rechenzentrum. Ermöglicht eine Dauerhaftigkeit von mindestens 99,999999999 Prozent (elf Neunen) für Objekte innerhalb eines bestimmten Jahrs. | Erwägen Sie, ob Ihre Anwendung Daten speichert, die problemlos wiederhergestellt werden können. |
| **Zonenredundanter Speicher (ZRS)** | Schützt vor Rechenzentrumsausfällen, indem über drei Speichercluster in einer einzelnen Region hinweg repliziert wird. Jeder Speichercluster ist physisch unabhängig und befindet sich in einer eigenen Verfügbarkeitszone. Ermöglicht eine Dauerhaftigkeit von mindestens 99,9999999999 Prozent (zwölf Neunen) für Objekte innerhalb eines bestimmten Jahrs, indem mehrere Kopien Ihrer Daten in mehreren Rechenzentren bzw. Regionen gespeichert werden. | Überlegen Sie, ob Sie Konsistenz, Dauerhaftigkeit und Hochverfügbarkeit benötigen. Schützt eventuell nicht vor einem regionalen Notfall, wenn mehrere Zonen dauerhaft betroffen sind. |
| **Georedundanter Speicher (GRS)** | Schützt vor dem Ausfall einer vollständigen Region, indem Daten in einer sekundären Region repliziert werden, die mehrere hundert Kilometer vom primären Speicherort der Quelldaten entfernt ist. Ermöglicht eine Dauerhaftigkeit von mindestens 99,99999999999999 Prozent (16 Neunen) für Objekte innerhalb eines bestimmten Jahrs. | Replikatdaten sind nur verfügbar, wenn Microsoft ein Failover in die sekundäre Region initiiert. Kommt es zu einem Failover, sind Lese- und Schreibzugriff verfügbar. |
| **Georedundanter Speicher mit Lesezugriff (RA-GRS)** | Ähnlich wie GRS. Ermöglicht eine Dauerhaftigkeit von mindestens 99,99999999999999 Prozent (16 Neunen) für Objekte innerhalb eines bestimmten Jahrs. | Ermöglicht außerdem 99,99 Prozent Leseverfügbarkeit, indem Lesezugriff aus der zweiten für GRS verwendeten Region zugelassen wird. |

**Weitere Informationen**:

- Sehen Sie sich die [Preise für Azure Storage](https://azure.microsoft.com/pricing/details/storage) an.
- Informieren Sie sich über [Azure Import/Export](https://docs.microsoft.com/azure/storage/common/storage-import-export-service).
- Vergleichen Sie [Datentypen für Blobs, Dateien und Datenträgerspeicher](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks).
- Informieren Sie sich genauer zu [Zugriffsebenen](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers).
- Erfahren Sie mehr über [verschiedene Typen von Speicherkonten](https://docs.microsoft.com/azure/storage/common/storage-account-overview).
- Informieren Sie sich zu [Azure Storage-Redundanz](https://docs.microsoft.com/azure/storage/common/storage-redundancy), einschließlich LRS, ZRS, GRS und GRS mit Lesezugriff.
- Weitere Informationen zu [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="best-practice-take-advantage-of-azure-hybrid-benefit"></a>Bewährte Methode: Nutzen von Azure-Hybridvorteil

Ein Portfolio, mit dem lokale Microsoft-Software mit Azure integriert wird, kann für Sie zu Wettbewerbs- und Kostenvorteilen führen. Wenn Sie zurzeit eine Betriebssystem- oder anderweitige Softwarelizenzierung über Software Assurance besitzen, können Sie diese Lizenzen mit in die Cloud nehmen, um den Azure-Hybridvorteil zu nutzen.

**Weitere Informationen**:

- [Werfen Sie einen Blick auf](https://azure.microsoft.com/pricing/hybrid-benefit) den Einsparungsrechner für Azure-Hybridvorteil.
- Weitere Informationen zu [Azure-Hybridvorteil für Windows Server](https://azure.microsoft.com/pricing/hybrid-benefit).
- Sehen Sie sich die [Preisinformationen für virtuelle Azure-Computer mit SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) an.

## <a name="best-practice-use-reserved-vm-instances"></a>Bewährte Methode: Reservierte VM-Instanzen verwenden

Für die meisten Cloudplattformen wird ein Modell mit nutzungsbasierter Bezahlung verwendet. Dieses Modell beinhaltet Nachteile, da Sie nicht unbedingt wissen, wie sich Ihre dynamischen Workloads entwickeln. Wenn Sie also klare Absichten für eine Workload formulieren, tragen Sie damit zur Infrastrukturplanung bei.

Bei Verwendung von Azure Reserved VM Instances zahlen Sie für VM-Instanzen 1 Jahr oder 3 Jahre im Voraus.

- Durch die Vorauszahlung erhalten Sie einen Rabatt für die verwendeten Ressourcen.
- Sie können die Kosten für VMs, Azure SQL-Datenbank-Compute-Instanzen, Azure Cosmos DB-Kapazitäten oder andere Ressourcen im Vergleich zur nutzungsbasierten Bezahlung deutlich senken.
- Reservierungen bieten einen Abrechnungsrabatt und wirken sich nicht auf den Laufzeitstatus Ihrer Ressourcen aus.
- Sie können reservierte Instanzen kündigen.

![Screenshot: Vergleich von nutzungsbasierter Bezahlung und Azure-Hybridvorteil mit reservierten Instanzen](./media/migrate-best-practices-costs/reserve.png)
_Abbildung 3: Azure Reserved VM Instances_

**Weitere Informationen**:

- Informieren Sie sich zu [Azure-Reservierungen](https://docs.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations).
- Lesen Sie [Azure Reserved VM Instances: Häufig gestellte Fragen](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq)
- Lesen Sie die [Preisinformationen für Azure-VMs mit SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="best-practice-aggregate-cloud-spending-across-subscriptions"></a>Bewährte Methode: Aggregieren der übergreifenden Cloudausgaben für Abonnements

Die Wahrscheinlichkeit ist relativ hoch, dass Sie über mehr als ein Azure-Abonnement verfügen. Beispielsweise könnten Sie ein zusätzliches Abonnement benötigen, um Entwicklungs- und Produktionsumgebungen voneinander zu trennen, oder Sie haben möglicherweise eine Plattform, die ein separates Abonnement für jeden Client erfordert. Die Möglichkeit zu besitzen, die Berichterstellung zu Daten über alle Abonnements hinweg in einer einzelnen Plattform zusammenzufassen, ist eine wertvolle Funktion.

Um dies zu erreichen, können Sie Azure Cost Management und Abrechnung-APIs verwenden. Nachdem Sie dann Daten in einer zentralen Quelle aggregiert haben, z. B. Azure SQL, können Sie diese Daten mit Tools wie Power BI bearbeiten. Sie können aggregierte Abonnementberichte sowie detaillierte Berichte erstellen. Für Benutzer, die proaktive Einblicke in das Kostenmanagement benötigen, können Sie beispielsweise spezifische Sichten für Kosten erstellen, gegliedert nach Abteilung, Ressourcengruppe oder anderen Informationen. Sie müssen ihnen dazu keinen Vollzugriff auf Azure-Abrechnungsdaten gewähren.

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure-Nutzungs-APIs](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview).
- Erfahren Sie mehr über das [Herstellen einer Verbindung mit Azure Consumption Insights in Power BI Desktop](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights).
- Informieren Sie sich darüber, wie Sie [den Zugriff auf Abrechnungsinformationen für Azure mithilfe der rollenbasierten Zugriffssteuerung (RBAC) verwalten](https://docs.microsoft.com/azure/billing/billing-manage-access).

## <a name="after-migration"></a>Nach der Migration

Im Anschluss an eine erfolgreiche Migration Ihrer Workloads und nach ein paar Wochen des Sammelns von Verbrauchsdaten haben Sie eine klare Vorstellung von den Kosten der Ressourcen. Parallel zur Analyse der Daten können Sie beginnen, eine Budgetbaseline für Azure-Ressourcengruppen und -Ressourcen zu generieren. Wenn Sie dann zunehmend herausfinden, wo Ihr Budget für die Cloud verbraucht wird, können Sie analysieren, wie Sie Ihre Kosten noch weiter senken können.

## <a name="best-practice-use-azure-cost-management-and-billing"></a>Bewährte Methode: Verwenden von Azure Cost Management und Abrechnung

Microsoft stellt „Azure Cost Management und Abrechnung“ bereit, um Ihnen bei der Nachverfolgung Ihrer Ausgaben zu helfen. Dieser Dienst:

- Unterstützt Sie bei der Überwachung und Kontrolle der Azure-Ausgaben sowie bei der Optimierung der Ressourcennutzung.
- Überprüft Ihr gesamtes Abonnement mit allen darin enthaltenen Ressourcen und gibt Empfehlungen.
- Stellt für Sie eine vollständige API bereit, um externe Tools und Finanzsysteme für die Berichterstellung zu integrieren.
- Verfolgt die Ressourcennutzung nach und ermöglicht Ihnen die Verwaltung der Cloudkosten in einer zentralen einheitlichen Ansicht.
- Bietet umfassende Erkenntnisse zu Betrieb und Finanzen, um Sie bei fundierten Entscheidungen zu unterstützen.

Mit Azure Cost Management und Abrechnung haben Sie folgende Möglichkeiten:

- Erstellen Sie ein Budget zur Wahrnehmung Ihrer finanziellen Verantwortung.
  - Sie können dabei Dienste berücksichtigen, die Sie für einen bestimmten Zeitraum verwenden oder abonnieren (monatlich, vierteljährlich oder jährlich), sowie einen Bereich (Abonnements oder Ressourcengruppen). Beispielsweise können Sie ein Azure-Abonnementbudget für den Zeitraum eines Monats, Quartals oder Jahres erstellen.
    - Nach der Erstellung eines Budgets wird es in einer Kostenanalyse angezeigt. Der Vergleich Ihres Budgets mit den aktuellen Ausgaben ist wichtig, wenn Sie Ihre Kosten und die Ausgaben analysieren.
  - Sie können auswählen, dass E-Mail-Benachrichtigungen gesendet werden, wenn Ihre Budgetschwellenwerte erreicht werden.
  - Sie können Kostenmanagementdaten zur Analyse nach Azure Storage exportieren.

  ![Screenshot: Cost Management-Budget](./media/migrate-best-practices-costs/budget.png)
  _Abbildung 4: Budget für Azure Cost Management und Abrechnung_

- Führen Sie eine Kostenanalyse durch, um Ihre Organisationskosten zu untersuchen und zu analysieren, damit Sie das Anfallen von Kosten besser verstehen und Ausgabentrends erkennen können.
  - Die Kostenanalyse ist für Enterprise Agreement-Benutzer verfügbar.
  - Sie können Kostenanalysedaten für eine Reihe von Bereichen, einschließlich nach Abteilung, Konto, Abonnement oder Ressourcengruppe, anzeigen.
  - Sie können eine Kostenanalyse abrufen, die Gesamtkosten für den aktuellen Monat und die akkumulierten täglichen Kosten anzeigt.

  ![Screenshot: Azure Cost Management-Analyse](./media/migrate-best-practices-costs/analysis.png)
  _Abbildung 5: Analyse von Azure Cost Management und Abrechnung_

- Erhalten Sie Advisor-Empfehlungen, die Ihnen zeigen, wie Sie die Effizienz optimieren und verbessern können.

**Weitere Informationen**:

- Lesen Sie die [Übersicht zu Azure Cost Management und Abrechnung](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview).
- Erfahren Sie, wie Sie [Cloudinvestitionen mit Azure Cost Management und Abrechnung optimieren](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices).
- Erfahren Sie mehr über [Berichte von Azure Cost Management und Abrechnung](https://docs.microsoft.com/azure/cost-management/use-reports).
- Erhalten Sie ein [Tutorial zum Optimieren von Kosten mithilfe von Empfehlungen](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations).
- Sehen Sie sich die [Azure Consumption-APIs](https://docs.microsoft.com/rest/api/consumption/budgets) an.

## <a name="best-practice-monitor-resource-utilization"></a>Bewährte Methode: Ressourcennutzung überwachen

In Azure bezahlen Sie für die Nutzung, also wenn Ressourcen tatsächlich genutzt werden, und Sie bezahlen nicht, wenn Sie sie nicht nutzen. Bei virtuellen Computern erfolgt die Abrechnung, wenn ein virtueller Computer zugeordnet wird, und nachdem die Zuordnung eines virtuellen Computers aufgehoben wurde, fallen keine Kosten mehr an. Unter Berücksichtigung dieses Aspekts sollten Sie verwendete VMs überwachen und die Größenanpassung von VMs überprüfen.

Bewerten Sie kontinuierlich Ihre VM-Workloads, um Baselines zu bestimmen. Wenn Ihre Workload beispielsweise montags bis freitags zwischen 8:00 und 18:00 Uhr stark genutzt wird, aber außerhalb dieser Zeiten nur sehr wenig, können Sie virtuelle Computer außerhalb der Spitzenzeiten herabstufen. Dies kann bedeuten, dass Sie VM-Größen ändern oder VM-Skalierungsgruppen zum automatischen Hoch- oder Herunterskalieren von VMs verwenden könnten. Einige Unternehmen lassen VMs „schlummern“, indem Sie sie nach einem Zeitplan betreiben, mit dem angegeben wird, wann sie verfügbar sein sollen und wann sie nicht benötigt werden.

Sie können die VM-Nutzung mithilfe von Microsoft-Tools überwachen, z. B. Azure Cost Management und Abrechnung, Azure Monitor und Azure Advisor. Drittanbietertools sind ebenfalls verfügbar.

> [!NOTE]
> Zusätzlich zur Überwachung virtueller Computer sollten Sie weitere Netzwerkressourcen, z. B. Azure ExpressRoute und Gateways für virtuelle Netzwerke, auf zu niedrige und zu hohe Nutzung überwachen.

**Weitere Informationen**:

- Lesen Sie Übersichten über [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) und [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview).
- [Erhalten Sie Azure Advisor-Empfehlungen zu Kosten](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations).
- Erfahren Sie, wie Sie [Kosten anhand von Empfehlungen optimieren](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations) und [unerwartete Gebühren vermeiden](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Erfahren Sie mehr über das [Toolkit zur Azure-Ressourcenoptimierung (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Bewährte Methode: Budgets für Ressourcengruppen implementieren

Häufig kann es nützlich sein, Kostengrenzen an Ressourcengruppen auszurichten. Ein Ressourcengruppenbudget hilft Ihnen bei der Nachverfolgung der zu einer Ressourcengruppe gehörigen Kosten. Sie können Warnungen auslösen und viele verschiedene Playbooks ausführen, wenn Sie Ihr Budget erreichen oder überschreiten.

**Weitere Informationen**:

- Informieren Sie sich über das [Verwalten von Kosten mit Azure-Budgets](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario).
- Sehen Sie sich ein Tutorial zum [Erstellen und Verwalten eines Azure-Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets) an.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Bewährte Methode: Azure Monitor-Aufbewahrung optimieren

Wenn Sie Ressourcen in Azure verschieben und die Diagnoseprotokollierung für sie aktivieren, generieren Sie eine Menge Protokolldaten. In der Regel werden diese Protokolldaten an ein Speicherkonto gesendet, das einem Log Analytics-Arbeitsbereich zugeordnet ist. Hier sind einige Tipps zur Optimierung der Azure Monitor-Aufbewahrung angegeben:

- Je länger der Aufbewahrungszeitraum der Protokolldaten ist, desto mehr Daten laufen bei Ihnen auf.
- Nicht alle Protokolldaten sind gleich, und einige Ressourcen generieren mehr Protokolldaten, als andere.
- Aufgrund von Bestimmungen und Compliance ist es wahrscheinlich, dass Sie Protokolldaten für manche Ressourcen länger als für andere aufbewahren müssen.
- Sie sollten sorgfältig abwägen zwischen der Optimierung Ihrer Kosten für die Protokollspeicherung und der Aufbewahrung der erforderlichen Protokolldaten.
- Wir empfehlen Ihnen, die Protokollierung sofort nach Abschluss einer Migration zu bewerten und einzurichten, damit Sie kein Geld für die Aufbewahrung unwichtiger Protokolle aufwenden.

**Weitere Informationen**:

- Erfahren Sie mehr über das [Überwachen der Nutzung und der geschätzten Kosten](https://docs.microsoft.com/azure/azure-monitor/platform/usage-estimated-costs).

## <a name="best-practice-optimize-storage"></a>Bewährte Methode: Speicher optimieren

Wenn Sie vor der Migration bewährte Methoden für die Auswahl von Speicher befolgt haben, ernten Sie wahrscheinlich einige Vorteile. Es können aber auch noch zusätzliche Speicherkosten vorhanden sein, die Sie noch weiter optimieren können. Im Laufe der Zeit veralten Blobs und Dateien. Daten werden eventuell nicht mehr verwendet, doch die gesetzliche Anforderungen können verlangen, dass Sie sie noch für einen bestimmten Zeitraum beibehalten müssen. Solche Daten müssen Sie also nicht unbedingt auf Hochleistungsspeicher lagern, den Sie für die ursprüngliche Migration verwendet haben.

Das Identifizieren und Verschieben veralteter Daten in kostengünstigere Speicherbereiche kann große Auswirkungen auf Ihr monatliches Speicherbudget und damit einhergehende Kosteneinsparungen haben. Azure bietet viele Möglichkeiten, um Ihnen bei der Identifizierung und anschließenden Speicherung dieser veralteten Daten zu helfen.

- Profitieren Sie von Zugriffsebenen für „Allgemeinen v2“-Speicher, indem Sie weniger wichtige Daten von der heißen Speicherebene zur kalten bzw. „Archiv“-Speicherebene verschieben.
- Verwenden Sie StorSimple zur Unterstützung beim Verschieben veralteter Daten, die auf benutzerdefinierten Richtlinien basieren.

**Weitere Informationen**:

- Informieren Sie sich genauer zu [Zugriffsebenen](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers).
- Lesen Sie die [Übersicht über StorSimple](https://docs.microsoft.com/azure/azure-monitor/overview).
- Sehen Sie sich die [Preise für StorSimple](https://azure.microsoft.com/pricing/details/storsimple) an.

## <a name="best-practice-automate-vm-optimization"></a>Bewährte Methode: VM-Optimierung automatisieren

Das Hauptziel für die Ausführung einer VM in der Cloud ist die Maximierung von CPU, Arbeitsspeicher und Datenträger, die davon verwendet werden. Wenn Sie VMs ermitteln, die nicht optimiert sind, oder wenn Sie häufige Zeiträume haben, in denen VMs nicht verwendet werden, ist es sinnvoll, diese entweder herunterzufahren oder sie mithilfe von VM-Skalierungsgruppen herunterzuskalieren.

Sie können einen virtuellen Computer mit Azure Automation, VM-Skalierungsgruppen, automatischem Herunterfahren und Skript- oder Drittanbieterlösungen optimieren.

**Weitere Informationen**:

- Erfahren Sie mehr über die [vertikale automatische Skalierung](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision).
- [Planen des automatischen Starts einer VM](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start).
- Informieren Sie sich über das [Starten oder Beenden von VMs außerhalb von Nutzungszeiten in Azure Automation](https://docs.microsoft.com/azure/automation/automation-solution-vm-management).
- Informieren Sie sich genauer zu [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) und dem [Toolkit zur Azure-Ressourcenoptimierung (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practices-use-azure-logic-apps-and-runbooks-with-budgets-api"></a>Bewährten Methoden: Verwenden von Azure Logic Apps und Runbooks mit der API für Budgets

Azure bietet eine REST-API, die Zugriff auf die Abrechnungsinformationen Ihres Mandanten hat. Sie können die API für Budgets verwenden, um externe Systeme und Workflows zu integrieren, die von Metriken ausgelöst werden, die Sie aus den API-Daten erstellen. Sie können Nutzungs- und Ressourcendaten mittels Pull in Ihre bevorzugten Datenanalysetools abrufen. Sie können die API für Budgets in Azure Logic Apps und Runbooks integrieren.

Mithilfe der Azure-Ressourcennutzungs- und -Gebührenkarten-APIs können Sie Ihre Kosten genau vorhersagen und verwalten. Die APIs werden als Ressourcenanbieter implementiert und sind in den APIs enthalten, die von Azure Resource Manager verfügbar gemacht werden.

**Weitere Informationen**:

- Informieren Sie sich über die [Azure-API für Budgets](https://docs.microsoft.com/rest/api/consumption/budgets).
- Gewinnen Sie Erkenntnisse zur Nutzung mit den [Azure-Abrechnungs-APIs](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview).

## <a name="best-practice-implement-serverless-technologies"></a>Bewährte Methode: Serverlose Technologien implementieren

VM-Workloads werden häufig im Ist-Zustand („wie besehen“) migriert, um Ausfallzeiten zu vermeiden. VMs können häufig Aufgaben hosten, die zeitweiliger Art sind, nur kurz bzw. im Wechsel ausgeführt werden oder viele Stunden dauern. Beispiele hierfür sind VMs, die geplante Aufgaben ausführen, z. B. die Windows-Aufgabenplanung oder PowerShell-Skripts. Wenn diese Aufgaben nicht ausgeführt werden, belegen Sie dennoch eine VM und verursachen Kosten für Datenträgerspeicher.

Nachdem Sie diese Arten von Aufgaben migriert und gründlich überprüft haben, können Sie dafür die Migration zu serverlosen Technologien erwägen, z. B. Azure Functions oder Batchaufträge. Mit diesen Lösungen können die Kosten gesenkt werden, und Sie müssen die VMs dann nicht mehr verwalten und warten.

**Weitere Informationen**:

- Informationen zu [Azure Functions](https://azure.microsoft.com/services/functions).
- Informationen zu [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über weitere Best Practices:

- [Bewährte Methoden](./migrate-best-practices-security-management.md) für Sicherheit und Verwaltung nach der Migration.
- [Best Practices](./migrate-best-practices-networking.md) für Netzwerkfunktionen nach der Migration.
