---
title: Kosten- und Größenanpassung von Azure-Ressourcen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den bewährten Methoden für die Kosten- und Größenanpassung von Ressourcen in Azure vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4ba4d1affb073b987c87886a119849b9772e2f2c
ms.sourcegitcommit: f7c7ffedcb1fcddb932d56c48e87776394dc75a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2020
ms.locfileid: "92437029"
---
<!-- docutune:casing ARO "standard HDD" -->

# <a name="best-practices-for-costing-and-sizing-resources-hosted-in-azure"></a>Bewährte Methoden für die Kosten- und Größenplanung von in Azure gehosteten Ressourcen

Unter Beachtung aller Fachrichtungen von Governance ist Kostenmanagement ein wiederkehrendes Thema auf Unternehmensebene. Durch Kostenoptimierung und Kostenmanagement können Sie den langfristigen Erfolg Ihrer Azure-Umgebung sicherstellen. Es ist entscheidend, dass alle Teams (Finanzen, Verwaltung und Teams für die Anwendungsentwicklung) die damit verbundenen Kosten verstehen und regelmäßig überprüfen.

> [!IMPORTANT]
> Die in diesem Artikel wiedergegebenen bewährten Methoden und Meinungen basieren auf Plattform- und --Dienstfunktionen in Azure, die zum Zeitpunkt der Niederschrift verfügbar waren. Features und Funktionen ändern sich im Laufe der Zeit. Nicht alle Empfehlungen betreffen Ihre Bereitstellung, wählen Sie daher aus, was für Ihre Situation am besten geeignet ist.

## <a name="best-practices-by-team-and-accountability"></a>Bewährte Methoden nach Team und Verantwortlichkeit

Das Kostenmanagement im gesamten Unternehmen ist eine Funktion von Cloudgovernance und Cloudvorgängen. Alle Entscheidungen des Kostenmanagements bewirken eine Änderung der Ressourcen, die eine Workload unterstützen. Wirken sich diese Änderungen auf die Architektur einer Workload aus, sind weitere Überlegungen anzustellen, um die Auswirkungen auf Endbenutzer und Geschäftsfunktionen zu minimieren. Das Cloudeinführungsteam, das diese Workload konfiguriert oder entwickelt hat, ist wahrscheinlich dafür zuständig, diese Arten von Änderungen abzuschließen.

- **Kennzeichnung (Tagging) ist für jede Art von Governance von entscheidender Bedeutung.** Stellen Sie sicher, dass bei allen Workloads und Ressourcen [ordnungsgemäße Benennungs- und Kennzeichnungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md) eingehalten werden, und [setzen Sie Kennzeichnungskonventionen mithilfe von Azure Policy durch](/azure/governance/policy/tutorials/govern-tags).
- **Bestimmen von Gelegenheiten zur richtigen Dimensionierung.** Überprüfen Sie Ihre aktuelle Ressourcennutzung und die Leistungsanforderungen in der gesamten Umgebung.
- **Ändern der Größe:** Ändern Sie jede Ressource so, dass sie die kleinste Instanz oder SKU verwendet, die die Leistungsanforderungen der jeweiligen Ressource unterstützen kann.
- **Horizontale vor vertikaler Skalierung.** Die Verwendung mehrerer kleiner Instanzen kann einen einfacheren Skalierungspfad als eine einzelne größere Instanz möglich machen. Dies ermöglicht automatische Skalierung, die zu Kostenoptimierung führt.

## <a name="operational-cost-management-best-practices"></a>Bewährte Methoden für das betriebliche Kostenmanagement

Die folgenden bewährten Methoden werden in der Regel von einem Mitglied des Cloudgovernance- oder Cloudbetriebsteams in Einklang mit Patching- und anderen geplanten Wartungsvorgängen befolgt. Diesen bewährten Methoden wird später in diesem Artikel ein handlungsrelevanter Leitfaden zugeordnet.

- **Kennzeichnung (Tagging) ist für jede Art von Governance von entscheidender Bedeutung:** Stellen Sie sicher, dass bei allen Workloads und Ressourcen [ordnungsgemäße Benennungs- und Kennzeichnungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md) eingehalten werden, und [setzen Sie Kennzeichnungskonventionen mithilfe von Azure Policy durch](/azure/governance/policy/tutorials/govern-tags).
- **Bestimmen von Gelegenheiten zur richtigen Dimensionierung:** Untersuchen Sie Ihre derzeitige Ressourcenauslastung und Leistungsanforderungen für die gesamte Umgebung, um Ressourcen zu ermitteln, die über einen längeren Zeitraum (normalerweise mehr als 90 Tage) nicht ausgelastet waren.
- **Richtige Dimensionierung bereitgestellter SKUs:** Ändern Sie eine nicht ausgelastete Ressource so, dass sie die kleinste Instanz oder SKU verwendet, die die Leistungsanforderungen der jeweiligen Ressource unterstützen kann.
- **Automatisches Herunterfahren für VMs:** Wird eine VM nicht durchgehend verwendet, sollten Sie das automatische Herunterfahren in Erwägung ziehen. Die VM wird nicht gelöscht und ihre Bereitstellung nicht aufgehoben, aber sie verursacht keine Compute- und Speicherkosten mehr, bis sie wieder eingeschaltet wird.
- **Automatisches Herunterfahren aller Nicht-Produktionsressourcen:** Wenn eine VM zu einer Nicht-Produktionsumgebung (insbesondere einer Entwicklungsumgebung) gehört, richten Sie eine Richtlinie zum automatischen Herunterfahren ein, um die Kosten für nicht verwendete Ressourcen zu senken. Verwenden Sie nach Möglichkeit Azure DevTest Labs als Self-Service-Option, um die Eigenverantwortlichkeit der Entwickler für Kosten zu fördern.
- **Herunterfahren und Außerbetriebnahme nicht verwendeter Ressourcen:** Ja, wir sagten es bereits. Wenn eine Ressource länger als 90 Tage lang nicht verwendet wurde und für sie keine eindeutige Betriebsbereitschaft-Anforderung besteht, schalten Sie sie aus. Noch wichtiger: Wenn ein Computer vor mehr als 90 Tagen beendet oder heruntergefahren wurde, heben Sie die Bereitstellung dieser Ressource auf, und löschen Sie sie. Überprüfen Sie, ob Datenaufbewahrungsrichtlinien durch Sicherungs- oder andere Mechanismen umgesetzt werden.
- **Bereinigen Sie verwaiste Datenträger:** Löschen Sie nicht verwendeten Speicher, insbesondere VM-Speicher, der keinen VMs mehr zugeordnet ist.
- **Richtige Dimensionierung von Redundanz:** Wenn die Ressource kein hohes Maß an Redundanz erfordert, entfernen Sie georedundanten Speicher.
- **Passen Sie Parameter für die automatische Skalierung an:** Bei der operativen Überwachung werden wahrscheinlich Verwendungsmuster für verschiedene Ressourcen aufgedeckt. Wenn diese Verwendungsmuster den Parametern zum Fördern der automatischen Skalierung zugeordnet werden, passt das Betriebsteam Parameter für die automatische Skalierung häufig entsprechend dem saisonalen Bedarf oder Änderungen von Budgetzuteilungen an. Informieren Sie sich unter den bewährten Methoden für das Kostenmanagement von Workloads über wichtige Vorsichtsmaßnahmen.

## <a name="workload-cost-management-best-practices"></a>Bewährte Methoden für das Kostenmanagement von Workloads

Bevor Sie Änderungen der Architektur vornehmen, sollten Sie sich mit dem technischen Leiter für die Workload besprechen. Es sollte eine Überprüfung der Workload mit der [Microsoft Azure Well-Architected Review](/assessments/?id=azure-architecture-review) und dem [Microsoft Azure Well-Architected Framework](/azure/architecture/framework) ausgeführt werden, um fundierte Entscheidungen zu den folgenden Architekturänderungen treffen zu können.

- **Azure App Service.** Überprüfen Sie die Produktionsanforderungen für alle App Service-Pläne im Premium-Tarif. Ohne ein Verständnis der geschäftlichen Anforderungen für eine Workload und der Konfiguration der zugrunde liegenden Ressourcen kann nur schwer festgestellt werden, ob ein Plan im Premium-Tarif erforderlich ist.
- **Horizontale vor vertikaler Skalierung.** Die Verwendung mehrerer kleiner Instanzen kann einen einfacheren Skalierungspfad als eine einzelne größere Instanz möglich machen. Dies ermöglicht automatische Skalierung, die zu Kostenoptimierung führt. Vor dem horizontalen Skalieren einer Workload muss das Technikerteam sicherstellen, dass die Anwendung idempotent ist. Für eine horizontale Skalierung müssen möglicherweise zuerst Änderungen am Code und an der Konfiguration verschiedener Anwendungsebenen vorgenommen werden.
- **Autoskalierung.** Aktivieren Sie die automatische Skalierung für alle App-Dienste, um kleinere virtuelle Computer in burstfähiger Anzahl vorzusehen. Für die Aktivierung der automatischen Skalierung gilt dieselbe idempotente Anforderung, wobei ein Verständnis der Workloadarchitektur erforderlich ist. Vor etwaigen operativen Änderungen muss das Einführungsteam die Workload und unterstützenden Ressourcen für horizontale Skalierung und automatische Skalierung genehmigen.
- **Implementieren serverloser Technologien:** VM-Workloads werden häufig im Istzustand („wie besehen“) migriert, um Ausfallzeiten zu vermeiden. Häufig hosten virtuelle Computer Aufgaben, die nur zwischenzeitlich ausgeführt werden und dafür nur einen kurzen Zeitraum beanspruchen, oder alternativ dazu viele Stunden. Beispielsweise VMs, die geplante Aufgaben ausführen, wie die Windows-Aufgabenplanung oder PowerShell-Skripts. Wenn diese Aufgaben nicht ausgeführt werden, belegen Sie dennoch eine VM und verursachen Kosten für Datenträgerspeicher. Erwägen Sie nach der Migration eine architekturbezogene Umstellung der Workloadebenen auf serverlose Technologien wie Azure Functions- oder Azure Batch-Aufträge.

## <a name="actionable-best-practices"></a>Umsetzbare bewährte Methoden

Im restlichen Teil dieses Artikels finden Sie taktische Beispiele für bewährte operative Methoden, die ein Cloudgovernance- oder Cloudbetriebsteam befolgen kann, um die Kosten im gesamten Unternehmen zu optimieren.

## <a name="before-adoption"></a>Vor der Einführung

Bevor Sie Ihre Workloads in die Cloud verschieben, schätzen Sie die monatlichen Kosten für ihren Betrieb in Azure ab. Die proaktive Verwaltung von Cloudkosten hilft Ihnen dabei, Ihr Budget für Betriebsaufwendungen einzuhalten. Die bewährten Methoden in diesem Abschnitt unterstützen Sie bei der Einschätzung der Kosten und bei der richtigen Dimensionierung von VMs und Speicher, bevor eine Workload in der Cloud bereitgestellt wird.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Bewährte Methode: Monatliche Workloadkosten abschätzen

Um eine Prognose für Ihre monatliche Rechnung für Azure-Ressourcen aufzustellen, gibt es eine Reihe von Tools, die Sie verwenden können.

<!-- TODO: Change "input costs" -->

- **Azure-Preisrechner:** Wählen Sie die Produkte aus, die Sie schätzen möchten, z. B. virtuelle Computer (VMs) und Speicher, und geben Sie dann im Rechner Kosten ein, um eine Schätzung zu erstellen.

    ![Azure-Preisrechner](../../migrate/azure-best-practices/media/migrate-best-practices-costs/pricing.png) *Azure-Preisrechner*

- **Azure Migrate:** Um Kosten zu schätzen, müssen Sie alle Ressourcen überprüfen und berücksichtigen, die für die Ausführung Ihrer Workloads in Azure erforderlich sind. Um diese Daten zu sammeln, erstellen Sie ein Inventar Ihrer Ressourcen, einschließlich Servern, virtueller Computer, Datenbanken und Speicher. Sie können Azure Migrate verwenden, um diese Informationen zu sammeln.
  - Azure Migrate ermittelt und bewertet Ihre lokale Umgebung, um ein Inventar aufzustellen.
  - Azure Migrate kann Abhängigkeiten zwischen VMs zuordnen und Ihnen aufzeigen, damit Sie ein vollständiges Bild erhalten.
  - Eine Azure Migrate-Bewertung enthält geschätzte Kosten.
    - **Computekosten:** Wenn Sie eine Bewertung erstellen, berechnet Azure Migrate anhand der empfohlenen Azure-VM-Größe und mithilfe der Azure-Abrechnungs-APIs die geschätzten monatlichen Kosten für den virtuellen Computer (VM-Kosten). Bei der Schätzung werden Betriebssystem, Software Assurance, Azure Reserved VM Instances, VM-Betriebszeit, Standort und Währungseinstellungen berücksichtigt. Die Kosten aller virtuellen Computer werden in der Bewertung zusammengefasst, um so die monatlichen Compute-Gesamtkosten zu berechnen.
    - **Speicherkosten:** Azure Migrate berechnet die monatlichen Speichergesamtkosten durch Aggregieren der Speicherkosten aller virtuellen Computer in einer Bewertung. Sie können die monatlichen Speicherkosten für einen bestimmten Computer berechnen, indem Sie die monatlichen Kosten aller an den Computer angefügten Datenträger zusammenfassen.

    ![Azure Migrate](../../migrate/azure-best-practices/media/migrate-best-practices-costs/assess.png)
    *Azure Migrate-Bewertung*

**Weitere Informationen** :

- Verwenden Sie den [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator).
- Sehen Sie sich die [Übersicht zu Azure Migrate](/azure/migrate/migrate-services-overview) an.
- Lesen Sie Informationen zu [Azure Migrate-Bewertungen](/azure/migrate/concepts-assessment-calculation).
- Erfahren Sie mehr über den [Azure Database Migration Service](/azure/dms/dms-overview).

## <a name="best-practice-right-size-vms"></a>Bewährte Methode: Richtige Größe von virtuellen Computern anpassen

Sie können eine Reihe von Optionen auswählen, wenn Sie virtuelle Azure-Computer bereitstellen, um Workloads zu unterstützen. Jeder VM-Typ verfügt über bestimmte Features und verschiedene Kombinationen aus CPU, Arbeitsspeicher und Datenträgern. VMs werden wie folgt gruppiert:

| type | Details | Verwendung |
|---|---|---|
| **Allgemeiner Zweck** | Ausgewogenes Verhältnis von CPU zu Arbeitsspeicher. | Gut geeignet für Tests und Entwicklung, kleine bis mittlere Datenbanken, Webserver mit geringer bis mittlerer Auslastung. |
| **Compute-optimiert** | Hohes Verhältnis von CPU zu Arbeitsspeicher. | Gut geeignet für mittlere Webserver, Network Appliances, Stapelverarbeitungsvorgänge, Anwendungsserver. |
| **Arbeitsspeicheroptimiert** | Hohes Verhältnis von Speicher zu CPU. | Gut geeignet für relationale Datenbanken, mittlere bis große Caches, In-Memory-Analysen. |
| **Speicheroptimiert** | Datenträgerdurchsatz und E/A-Vorgänge auf hohem Niveau. | Geeignet für Big Data sowie SQL- und NoSQL-Datenbanken. |
| **GPU-optimiert** | Spezialisierte VMs. Einzelne oder mehrere GPUs. | Anspruchsvolle Grafik- und Videobearbeitung. |
| **Hohe Leistung** | Schnellste und leistungsfähigste CPU. VMs mit optionalen Netzwerkschnittstellen mit hohem Durchsatz (RDMA). | Kritische Hochleistungsanwendungen. |

- Es ist wichtig, die Preisunterschiede zwischen diesen virtuellen Computern zu verstehen sowie die langfristigen Auswirkungen auf das Budget.
- Jeder Typ umfasst eine bestimmte Anzahl darin enthaltener VM-Serien.
- Außerdem können Sie, wenn Sie eine VM innerhalb einer Serie auswählen, die VM nur innerhalb dieser Serie zentral hoch- oder herunterskalieren. Eine `DS2_v2`-Instanz kann beispielsweise bis zu `DS4_v2` hochskaliert werden, aber sie kann nicht in eine Instanz einer anderen Serie, z. B. eine `F2S_v2`-Instanz, geändert werden.

**Weitere Informationen** :

- Erfahren Sie mehr zu [VM-Typen und -Größenanpassung](/azure/virtual-machines/windows/sizes) sowie zur Zuordnung von Größen zu Typen.
- Planen der [VM-Dimensionierung](/azure/cloud-services/cloud-services-sizes-specs).
- Arbeiten Sie eine [Beispielbewertung für das fiktive Unternehmen Contoso](../../plan/contoso-migration-assessment.md) durch.

## <a name="best-practice-select-the-right-storage"></a>Bewährte Methode: Den richtigen Speicher auswählen

Das Optimieren und Verwalten von lokalem Speicher (SAN oder NAS) sowie der Netzwerke, die diesen unterstützen, können teuer und zeitaufwendig sein. Datei(Speicher)daten werden häufig zur Cloud migriert, um Schwierigkeiten beim Betrieb und der Verwaltung zu beseitigen. Microsoft bietet verschiedene Optionen zum Verschieben von Daten in Azure, und Sie müssen sich hinsichtlich dieser Optionen entscheiden. Die Auswahl des richtigen Speichertyps für Daten kann Ihrer Organisation jeden Monat mehrere tausend Euro sparen. Ein paar Überlegungen:

- Daten, auf die nur selten zugegriffen wird und die nicht unternehmenskritisch sind, sollten nicht im teuersten Speicher platziert werden.
- Umgekehrt sollten sich unternehmenskritische Daten auf Speicheroptionen eines höheren Tarifs befinden.
- Erstellen Sie im Rahmen der Einführungsplanung ein Inventar der Daten, und klassifizieren Sie sie nach Wichtigkeit, um sie dem jeweils optimal geeigneten Speicher zuzuordnen. Berücksichtigen Sie hierbei Budget und Kosten sowie die Leistung. Kosten sollte nicht notwendigerweise der ausschlaggebende Entscheidungsfaktor sein. Die Entscheidung für die kostengünstigste Option könnte die Workload Leistungs- und Verfügbarkeitsrisiken aussetzen.

### <a name="storage-data-types"></a>Speicherdatentypen

Azure bietet verschiedene Arten von Speicherdaten.

| Datentyp | Details | Verwendung |
| ---|---|---|
| **Blobs** | Optimiert für die Speicherung großer Mengen von unstrukturierten Objekten wie z. B. Text- oder Binärdaten. | Zugriff auf Daten von überall her über HTTP/HTTPS. <br><br> Verwendung für Szenarios mit Streaming und wahlfreiem Zugriff. Beispielsweise um einem Browser Bilder und Dokumente direkt bereitzustellen, Video und Audio zu streamen und Sicherungs- und Notfallwiederherstellungsdaten zu speichern. |
| **Dateien** | Verwaltete Dateifreigaben, auf die über SMB 3.0 zugegriffen wird. | Verwendung beim Migrieren lokaler Dateifreigaben sowie zur Bereitstellung von mehrfachem Zugriff und mehreren Verbindungen, um Daten abzulegen. |
| **Datenträger** | Basierend auf Seitenblobs. <br><br> Datenträgertyp (Geschwindigkeit): HDD Standard, SSD Standard, SSD Premium oder Ultra Disks. <br><br> Datenträgerverwaltung: Nicht verwaltet (Sie verwalten Datenträgereinstellungen und Speicher) oder verwaltet (Sie wählen den Datenträgertyp aus, und Azure verwaltet diesen Datenträger für Sie). | Verwendung von Premium-Datenträgern für VMs. Verwendung von verwalteten Datenträgern für einfache Verwaltung und Skalierung. |
| **Warteschlangen** | Speichern und Abrufen großer Mengen von Nachrichten mittels Zugriff über authentifizierte Aufrufe (HTTP oder HTTPS). | Verbinden von Anwendungskomponenten mit asynchronem Message Queuing. |
| **Tabellen** | Speichern von Tabellen. | Jetzt Teil der Azure Cosmos DB-Tabellen-API. |

### <a name="access-tiers"></a>Zugriffsebenen

Azure Storage bietet verschiedene Optionen für den Zugriff auf Blockblobdaten. Die Auswahl der richtigen Zugriffsebene hilft sicherzustellen, dass Sie Blockblobdaten auf möglichst kostengünstige Art und Weise speichern.

| Zugriffsebene | Details | Verwendung |
| --- | --- | --- |
| **Heiße Ebene** | Höhere Speicherkosten, geringere Zugriffs- und Transaktionskosten <br><br> Dies ist die Standardzugriffsebene. | Verwendung für Daten, die aktiv und mit häufigem Zugriff verwendet werden. |
| **Kalte Ebene** | Geringere Speicherkosten, höhere Zugriffs- und Transaktionskosten. <br><br> Speicherung für mindestens 30 Tage. | Kurzfristige Speicherung, Daten sind verfügbar, aber Zugriff erfolgt nur selten. |
| **Archivieren** | Verwendung für einzelne Blockblobs. <br><br> Kostengünstigste Option für Speicherung. Niedrigste Speicherkosten, höchste Zugriffs- und Transaktionskosten. | Verwenden Sie sie für Daten, die mehrere Stunden Abrufwartezeit tolerieren und sich mindestens 180 Tage lang auf der Archivspeicherebene befinden werden. |

### <a name="storage-account-types"></a>Speicherkontotypen

Azure bietet verschiedene Typen von Speicherkonten und Leistungsstufen.

| Kontotyp | Details | Verwendung |
| --- | --- | --- |
| **Stufe „Universell V2 Standard“** | Unterstützt Blobs (Block, Seiten, Anfüge), Dateien, Datenträger, Warteschlangen und Tabellen. <br><br> Unterstützt die Zugriffsebenen „Heiß“, „Kalt“ und „Archiv“. Zonenredundanter Speicher (ZRS) wird unterstützt. | Verwendung für die meisten Szenarios und die meisten Typen von Daten. Standardspeicherkonten können auf HDDs oder SSDs basieren. |
| **Stufe „Universell V2 Premium“** | Unterstützt die Blobspeicherdaten (Seitenblobs). Unterstützt die Zugriffsebenen „Heiß“, „Kalt“ und „Archiv“. ZRS wird unterstützt. <br><br> Speicherung auf SSDs. | Microsoft empfiehlt die Verwendung für alle VMs. |
| **Universell V1** | Zugriffsebenen werden nicht unterstützt. Keine Unterstützung von ZRS. | Verwendung, wenn Anwendungen das klassische Azure-Bereitstellungsmodell benötigen. |
| **Blob** | Spezialisiertes Speicherkonto zum Speichern unstrukturierter Objekte. Bietet nur Blockblobs und Anfügeblobs (keine Datei-, Warteschlangen-, Tabellen- oder Datenträgerspeicherdienste). Bietet dieselbe Dauerhaftigkeit, Verfügbarkeit, Skalierbarkeit und Leistung wie „Universell V2“. | Sie können in diesen Konten keine Seitenblobs und deshalb auch keine VHD-Dateien speichern. Sie können eine Zugriffsebene auf „Heiß“ oder „Kalt“ festlegen. |

### <a name="storage-redundancy-options"></a>Redundanzoptionen für Storage

Speicherkonten können verschiedene Arten von Redundanz für Resilienz und Hochverfügbarkeit verwenden.

| type | Details | Verwendung |
| --- | --- | --- |
| **Lokal redundanter Speicher (LRS)** | Schützt vor einem lokalen Ausfall durch Replikation in eine einzelne Speichereinheit in einer gesonderten Fehler- und Updatedomäne. Behält mehrere Kopien Ihrer Daten in einem Rechenzentrum. Stellt eine Dauerhaftigkeit von mindestens 99,999999999 Prozent (11 Neunen) für Objekte in einem bestimmten Jahr bereit. | Erwägen Sie, ob Ihre Anwendung Daten speichert, die problemlos wiederhergestellt werden können. |
| **Zonenredundanter Speicher (ZRS)** | Schützt vor Rechenzentrumsausfällen, indem über drei Speichercluster in einer einzelnen Region hinweg repliziert wird. Jeder Speichercluster ist physisch unabhängig und befindet sich in einer eigenen Verfügbarkeitszone. Bietet eine Dauerhaftigkeit von mindestens 99,9999999999 Prozent (12 Neunen) für Objekte für ein bestimmtes Jahr, indem mehrere Kopien Ihrer Daten in mehreren Rechenzentren oder mehreren Regionen gespeichert werden. | Überlegen Sie, ob Sie Konsistenz, Dauerhaftigkeit und Hochverfügbarkeit benötigen. Schützt eventuell nicht vor einem regionalen Notfall, wenn mehrere Zonen dauerhaft betroffen sind. |
| **Georedundanter Speicher (GRS)** | Schützt vor dem Ausfall einer vollständigen Region, indem Daten in eine sekundäre Region repliziert werden, die mehrere hundert Kilometer vom primären Speicherort der Quelldaten entfernt ist. Stellt eine Dauerhaftigkeit von mindestens 99,99999999999999 Prozent (16 Neunen) für Objekte in einem bestimmten Jahr bereit. | Replikatdaten sind nur verfügbar, wenn Microsoft ein Failover in die sekundäre Region initiiert. Kommt es zu einem Failover, sind Lese- und Schreibzugriff verfügbar. |
| **Georedundanter Speicher mit Lesezugriff (RA-GRS)** | Ähnlich wie GRS. Stellt eine Dauerhaftigkeit von mindestens 99,99999999999999 Prozent (16 Neunen) für Objekte in einem bestimmten Jahr bereit. | Bietet außerdem 99,99 Prozent Leseverfügbarkeit, indem Lesezugriff aus der zweiten für GRS verwendeten Region zugelassen wird. |

**Weitere Informationen** :

- Sehen Sie sich die [Preise für Azure Storage](https://azure.microsoft.com/pricing/details/storage) an.
- Erfahren Sie mehr über das Verwenden des [Azure Import/Export-Diensts](/azure/storage/common/storage-import-export-service), um große Datenmengen sicher in Azure Blob Storage und Azure Files zu importieren.
- Vergleichen Sie [Datentypen für Blobs, Dateien und Datenträgerspeicher](/azure/storage/common/storage-introduction).
- Informieren Sie sich genauer zu [Zugriffsebenen](/azure/storage/blobs/storage-blob-storage-tiers).
- Erfahren Sie mehr über [verschiedene Typen von Speicherkonten](/azure/storage/common/storage-account-overview).
- Informieren Sie sich zu [Azure Storage-Redundanz](/azure/storage/common/storage-redundancy), einschließlich LRS, ZRS, GRS und GRS mit Lesezugriff.
- Weitere Informationen zu [Azure Files](/azure/storage/files/storage-files-introduction).

## <a name="after-adoption"></a>Nach der Einführung

Vor der Einführung sind die Kostenprognosen von Entscheidungen abhängig, die von Workloadbesitzern und dem Team zur Cloudeinführung getroffen werden. Das Governanceteam hat zwar einen gewissen Einfluss auf diese Entscheidungen, ihm werden sich aber wahrscheinlich wenig Handlungsmöglichkeiten bieten.

Sobald sich die Ressourcen im Produktionsbetrieb befinden, können Daten aggregiert und Trends auf Unternehmensebene analysiert werden. Diese Daten helfen dem Governanceteam beim Treffen unabhängiger Dimensionierungs- und Nutzungsentscheidungen auf der Grundlage tatsächlicher Verwendungsmuster und der aktuellen Zustandsarchitektur.

- Analysieren Sie die Daten, um eine Budgetbaseline für Azure-Ressourcengruppen und -Ressourcen zu generieren.
- Identifizieren Sie Verwendungsmuster. Dies ermöglicht es Ihnen, die Größe von Ressourcen zu verringern und Ressourcen anzuhalten oder zu beenden, um Ihre Kosten weiter zu senken.

Bewährte Methoden in diesem Abschnitt umfassen die Nutzung von Azure-Hybridvorteil und Azure Reserved Virtual Machine Instances, das Senken von Cloudausgaben für alle Abonnements, die Verwendung von Azure Cost Management + Billing für die Budgetierung und Analyse von Kosten, die Überwachung von Ressourcen und Implementierung von Budgets für Ressourcengruppen sowie die Optimierung von Überwachung, Speicher und VMs.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefit"></a>Bewährte Methode: Nutzen von Azure-Hybridvorteil

Dank jahrelanger Investitionen in Softwaresysteme wie Windows Server und SQL Server befindet sich Microsoft in der einzigartigen Lage, Kunden Wertschöpfung in der Cloud mit beträchtlichen Rabatte anbieten zu können, die andere Cloudanbieter nicht unbedingt bereitstellen können.

Eine integriertes Portfolio aus lokalen und Azure-Produkten von Microsoft generiert Wettbewerbs- und Kostenvorteile. Wenn Sie zurzeit eine Betriebssystem- oder anderweitige Softwarelizenzierung durch Software Assurance (SA) besitzen, können Sie diese Lizenzen mit in die Cloud nehmen, um Azure-Hybridvorteil zu nutzen.

**Weitere Informationen** :

- [Werfen Sie einen Blick auf](https://azure.microsoft.com/pricing/hybrid-benefit) den Einsparungsrechner für Azure-Hybridvorteil.
- Weitere Informationen zu [Azure-Hybridvorteil für Windows Server](https://azure.microsoft.com/pricing/hybrid-benefit).
- Sehen Sie sich die [Preisinformationen für virtuelle Azure-Computer mit SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) an.

## <a name="best-practice-use-azure-reserved-vm-instances"></a>Bewährte Methode: Verwenden von Azure Reserved VM Instances

Die meisten Cloudplattformen sind mit nutzungsbasierter Bezahlung eingerichtet. Dieses Modell beinhaltet Nachteile, da Sie nicht unbedingt wissen, wie sich dynamische Arbeitslasten entwickeln. Wenn Sie also klare Absichten für eine Workload formulieren, tragen Sie damit zur Infrastrukturplanung bei.

Wenn Sie Azure Reserved VM Instances verwenden, zahlen Sie für reservierte Instanzen entweder 1 Jahr oder 3 Jahre im Voraus.

- Durch die Vorauszahlung erhalten Sie einen Rabatt für die verwendeten Ressourcen.
- Sie können die Kosten für VM-Compute, SQL-Datenbank-Compute, Azure Cosmos DB oder andere Ressourcen deutlich um bis zu 72  % gegenüber der nutzungsbasierten Bezahlung senken.
- Reservierte Instanzen bieten einen Abrechnungsrabatt und wirken sich nicht auf den Laufzeitstatus Ihrer Ressourcen aus.
- Sie können reservierte Instanzen kündigen.

![Azure Reserved Virtual Machine Instances](../../migrate/azure-best-practices/media/migrate-best-practices-costs/reserve.png)
*Abbildung 1: Reservierte Azure-VMs.*

**Weitere Informationen** :

- Informieren Sie sich zu [Azure-Reservierungen](/azure/cost-management-billing/reservations/save-compute-costs-reservations).
- Lesen Sie [Häufig gestellte Fragen zu reservierten Instanzen](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq).
- Sehen Sie sich die [Preisinformationen für virtuelle Azure-Computer mit SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) an.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Bewährte Methode: Cloudausgaben über Abonnements hinweg akkumulieren

Es ist unvermeidlich, dass Sie letztendlich mehr als ein Azure-Abonnement haben werden. Beispielsweise könnten Sie ein zusätzliches Abonnement benötigen, um Entwicklungs- und Produktionsumgebungen voneinander zu trennen, oder Sie haben möglicherweise eine Plattform, die ein separates Abonnement für jeden Client erfordert. Die Möglichkeit zu besitzen, die Berichterstellung zu Daten über alle Abonnements hinweg in einer einzelnen Plattform zusammenzufassen, ist eine wertvolle Funktion.

Um dies zu erreichen, können Sie Azure Cost Management + Billing-APIs verwenden. Nachdem Sie dann Daten in einer zentralen Quelle aggregiert haben, z. B. Azure SQL-Datenbank, können Sie diese Daten mit Tools wie Power BI bearbeiten. Sie können aggregierte Abonnementberichte sowie detaillierte Berichte erstellen. Für Benutzer, die proaktive Einblicke in das Kostenmanagement benötigen, können Sie beispielsweise spezifische Sichten für Kosten erstellen, gegliedert nach Abteilung, Ressourcengruppe oder anderen Informationen. Sie müssen ihnen dazu keinen Vollzugriff auf Azure-Abrechnungsdaten gewähren.

**Weitere Informationen** :

- Lesen Sie die [Übersicht über Azure-Nutzungs-APIs](/azure/billing/billing-consumption-api-overview).
- Erfahren Sie mehr über das [Herstellen einer Verbindung mit Azure Consumption Insights in Power BI Desktop](/power-bi/desktop-connect-azure-consumption-insights).
- Erfahren Sie, wie Sie [den Zugriff auf Abrechnungsinformationen für Azure mithilfe der rollenbasierten Zugriffssteuerung (RBAC) verwalten](/azure/billing/billing-manage-access).

## <a name="best-practice-monitor-resource-utilization"></a>Bewährte Methode: Ressourcennutzung überwachen

In Azure bezahlen Sie für die Nutzung, also wenn Ressourcen tatsächlich genutzt werden, und Sie bezahlen nicht, wenn Sie sie nicht nutzen. Bei virtuellen Computern erfolgt die Abrechnung, wenn ein virtueller Computer zugeordnet wird, und nachdem die Zuordnung eines virtuellen Computers aufgehoben wurde, fallen keine Kosten mehr an. Unter Berücksichtigung dieses Aspekts sollten Sie verwendete VMs überwachen und die Größenanpassung von VMs überprüfen.

- Bewerten Sie kontinuierlich Ihre VM-Workloads, um Baselines zu bestimmen.
- Wenn Ihre Workload beispielsweise montags bis freitags zwischen 8: 00 und 18 Uhr stark verwendet wird, außerhalb dieser Zeiten jedoch kaum, könnten Sie virtuelle Computer außerhalb der Spitzenzeiten herabstufen. Dies kann bedeuten, dass Sie VM-Größen ändern oder VM-Skalierungsgruppen zum automatischen Hoch- oder Herunterskalieren von VMs verwenden könnten.
- Einige Unternehmen lassen VMs „schlummern“, indem Sie sie nach einem Zeitplan betreiben, der angibt, wann sie verfügbar sein sollten und wann sie nicht benötigt werden.
- Zusätzlich zur Überwachung virtueller Computer sollten Sie weitere Netzwerkressourcen wie ExpressRoute und Gateways für virtuelle Netzwerke auf zu niedrige und zu hohe Nutzung überwachen.
- Sie können die VM-Nutzung mithilfe von Microsoft-Tools überwachen, wie z. B. Azure Cost Management + Billing, Azure Monitor und Azure Advisor. Drittanbietertools sind ebenfalls verfügbar.

**Weitere Informationen** :

- Lesen Sie Übersichten über [Azure Monitor](/azure/azure-monitor/overview) und [Azure Advisor](/azure/advisor/advisor-overview).
- Erhalten Sie [Azure Advisor-Empfehlungen zu Kosten](/azure/advisor/advisor-cost-recommendations).
- Erfahren Sie, wie Sie [Kosten anhand von Empfehlungen optimieren](/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations) und [unerwartete Gebühren vermeiden](/azure/billing/billing-getting-started).
- Erfahren Sie mehr über das [Toolkit zur Azure-Ressourcenoptimierung (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-reduce-nonproduction-costs"></a>Bewährte Methode: Senken nicht produktionsbezogener Kosten

Während der Entwicklungszyklen werden Umgebungen für Entwicklung, Tests und Qualitätssicherung (QS) benötigt. Leider kommt es häufig vor, dass diese Umgebungen noch lange nach dem Ende ihrer Nutzung bereitgestellt bleiben. Eine regelmäßige Überprüfung der nicht verwendeten Nichtproduktionsumgebungen kann sich unmittelbar auf die Kosten auswirken.

Ziehen Sie darüber hinaus allgemeine Kosteneinsparungen für alle Nichtproduktionsumgebungen in Betracht:

- Stufen Sie Nichtproduktionsressourcen auf kostengünstigere VMs der B-Serie und Standardspeicher herab.
- Senken Sie mithilfe von Spot-VMs die nicht produktionsbezogenen Computekosten.
- Wenden Sie Azure-Richtlinien an, um Kostensenkungen für alle Nichtproduktionsressourcen auf Ressourcenebene vorzuschreiben.

**Weitere Informationen** :

- [Verwenden Sie Tags](/azure/azure-resource-manager/management/tag-resources), um Entwicklungs-, Test- oder QA-Ziele zum Ändern der Dimensionierung oder Beendigung zu kennzeichnen.
- [Automatisches Herunterfahren von VMs](/azure/cost-management-billing/manage/getting-started#consider-cost-cutting-features-like-auto-shutdown-for-vms) legt eine nächtliche Beendigungszeit für VMs fest. Durch Verwendung dieses Features werden Nicht-Produktions-VMs jede Nacht gestoppt, sodass Entwickler diese VMs neu starten müssen, wenn sie zur Fortsetzung der Entwicklungsarbeit bereit sind.
- Mithilfe von [Spot-VMs](/azure/virtual-machines/spot-vms) können Sie ungenutzte Azure-Kapazität mit signifikanten Kosteneinsparungen nutzen. Wenn jedoch die Kapazität von Azure wieder benötigt wird, werden die Spot-VMs durch die Azure-Infrastruktur entfernt.
- Ermutigen Sie Entwicklungsteams, [Azure DevTest Labs](/azure/lab-services/devtest-lab-overview) zu nutzen, um eigene Ansätze zur Kostenkontrolle zu entwickeln und Beeinträchtigungen durch die Standardzeitvorgaben für automatisches Herunterfahren im vorherigen Schritt zu vermeiden.

## <a name="best-practice-use-azure-cost-management--billing"></a>Bewährte Methode: Verwenden von Azure Cost Management + Billing

Microsoft stellt Azure Cost Management + Billing bereit, um Ihnen bei der Nachverfolgung Ihrer Ausgaben zu helfen.

- Unterstützt Sie bei der Überwachung und Kontrolle der Azure-Ausgaben sowie bei der Optimierung der Ressourcennutzung.
- Überprüft Ihr gesamtes Abonnement mit allen darin enthaltenen Ressourcen und gibt Empfehlungen.
- Bietet eine vollständige API, um externe Tools und Finanzsysteme für die Berichterstellung zu integrieren.
- Verfolgt die Ressourcennutzung und Verwaltet Cloudkosten mit einer einzigen, einheitlichen Ansicht.
- Bietet umfassende Erkenntnisse zu Betrieb und Finanzen, um Sie bei fundierten Entscheidungen zu unterstützen.

In Azure Cost Management + Billing haben Sie folgende Möglichkeiten:

- **Ein Budget erstellen:** Erstellen Sie ein Budget zur Wahrnehmung Ihrer finanziellen Verantwortung.
  - Sie können dabei Dienste berücksichtigen, die Sie für einen bestimmten Zeitraum verwenden oder abonnieren (monatlich, vierteljährlich, jährlich), sowie einen Bereich (Abonnements/Ressourcengruppen). Beispielsweise können Sie ein Azure-Abonnementbudget für den Zeitraum eines Monats, Quartals oder Jahres erstellen.
    - Nach der Erstellung eines Budgets wird es in der Kostenanalyse angezeigt. Die Betrachtung Ihres Budgets in Bezug auf Ihre aktuellen Ausgaben ist einer der ersten Schritte, die zur Analyse Ihrer Kosten und Ausgaben erforderlich sind.
  - Sie können E-Mail-Benachrichtigungen versenden lassen, wenn Budgetschwellenwerte erreicht werden.
  - Sie können Kostenmanagementdaten zur Analyse nach Azure Storage exportieren.

    ![Anzeigen von Budgets in Azure Cost Management + Billing](../../migrate/azure-best-practices/media/migrate-best-practices-costs/budget.png)
    *Budgets in Azure Cost Management + Billing* .

- **Eine Kostenanalyse durchführen:** Stellen Sie eine Kostenanalyse auf, um Ihre Organisationskosten zu untersuchen und zu analysieren, damit Sie besser verstehen, wie Kosten anfallen, und Ausgabentrends erkennen können.
  - Die Kostenanalyse steht EA-Benutzern zur Verfügung.
  - Sie können Kostenanalysedaten für eine Reihe von Bereichen, einschließlich nach Abteilung, Konto, Abonnement oder Ressourcengruppe, anzeigen.
  - Sie können eine Kostenanalyse abrufen, die Gesamtkosten für den aktuellen Monat und die akkumulierten täglichen Kosten anzeigt.

    ![Analyse von Azure Cost Management + Billing](../../migrate/azure-best-practices/media/migrate-best-practices-costs/analysis.png)
    *Abbildung: Analyse von Azure Cost Management + Billing*

- **Empfehlungen abrufen:** Erhalten Sie Advisor-Empfehlungen, die Ihnen zeigen, wie Sie die Effizienz optimieren und verbessern können.

**Weitere Informationen** :

- Lesen Sie die [Übersicht zu Azure Cost Management + Billing](/azure/cost-management/overview).
- Erfahren Sie mehr zum [Optimieren der Cloudinvestitionen mit Azure Cost Management + Billing](/azure/cost-management-billing/costs/cost-mgt-best-practices).
- Erfahren Sie mehr über die Verwendung der [Berichte von Azure Cost Management + Billing](/azure/cost-management/use-reports).
- Sehen Sie sich ein Tutorial zum [Optimieren von Kosten mithilfe von Empfehlungen](/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations) an.
- Sehen Sie sich die [Azure Consumption-APIs](/rest/api/consumption/budgets) an.

## <a name="best-practice-implement-resource-group-budgets"></a>Bewährte Methode: Budgets für Ressourcengruppen implementieren

Häufig werden Ressourcengruppen verwendet, um Kostengrenzen darzustellen. Zusammen mit diesem Verwendungsmuster entwickelt das Azure-Team weiterhin neue und verbesserte Möglichkeiten zum Nachverfolgen und Analysieren der Ressourcenausgaben auf unterschiedlichen Ebenen, einschließlich der Möglichkeit zur Erstellung von Budgets für Ressourcengruppen und Ressourcen.

- Ein Ressourcengruppenbudget hilft Ihnen bei der Nachverfolgung der zu einer Ressourcengruppe gehörigen Kosten.
- Sie können außerdem Benachrichtigungen auslösen und eine Vielzahl von Playbooks ausführen, wenn das Budget erreicht oder überschritten wird.

**Weitere Informationen** :

- Informieren Sie sich über das [Verwalten von Kosten mit Azure-Budgets](/azure/billing/billing-cost-management-budget-scenario).
- Sehen Sie sich ein Tutorial zum [Erstellen und Verwalten eines Azure-Budgets](/azure/cost-management-billing/costs/tutorial-acm-create-budgets) an.

## <a name="best-practice-review-azure-advisor-recommendations"></a>Bewährte Methode: Arbeiten Sie Azure Advisor-Empfehlungen durch

Azure Advisor-Empfehlungen zu Kosten benennen Möglichkeiten zur Kostensenkung. Wenn das Budget hoch oder die Auslastung niedrig erscheint, finden Sie in diesem Bericht unmittelbare Möglichkeiten, um die Kosten schnell anzupassen.

**Weitere Informationen** :

- [Arbeiten Sie Azure Advisor-Empfehlungen zu Kosten durch](/azure/advisor/advisor-cost-recommendations), um sofort Maßnahmen zu ergreifen.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Bewährte Methode: Azure Monitor-Aufbewahrung optimieren

Wenn Sie Ressourcen in Azure verschieben und die Diagnoseprotokollierung für sie aktivieren, generieren Sie eine Menge Protokolldaten. In der Regel werden diese Protokolldaten an ein Speicherkonto gesendet, das einem Log Analytics-Arbeitsbereich zugeordnet ist.

- Je länger der Aufbewahrungszeitraum der Protokolldaten ist, desto mehr Daten laufen bei Ihnen auf.
- Nicht alle Protokolldaten sind gleich, und einige Ressourcen generieren mehr Protokolldaten, als andere.
- Aufgrund von Bestimmungen und Compliance ist es wahrscheinlich, dass Sie Protokolldaten für manche Ressourcen länger aufbewahren müssen, als für andere.
- Wägen Sie zwischen der Optimierung Ihrer Kosten für die Protokollspeicherung und der Aufbewahrung der erforderlichen Protokolldaten ab.
- Wir empfehlen, dass Sie die Protokollierung sofort nach Abschluss einer Migration bewerten und einrichten, damit Sie kein Geld dafür aufwenden, unwichtige Protokolle aufzubewahren.

**Weitere Informationen** :

- Erfahren Sie mehr über das [Überwachen der Nutzung und der geschätzten Kosten](/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs).

## <a name="best-practice-optimize-storage"></a>Bewährte Methode: Speicher optimieren

Wenn Sie vor der Einführung bewährte Methoden für die Auswahl von Speicher befolgt haben, profitieren Sie wahrscheinlich von einigen Vorteilen. Sie können wahrscheinlich noch zusätzliche Speicherkosten optimieren. Im Laufe der Zeit veralten Blobs und Dateien. Daten werden eventuell nicht mehr verwendet, doch die gesetzliche Anforderungen können verlangen, dass Sie sie noch für einen bestimmten Zeitraum beibehalten müssen. Solche Daten müssen Sie also nicht unbedingt auf Hochleistungsspeicher lagern, den Sie für die ursprüngliche Einführung verwendet haben.

Das Identifizieren und Verschieben veralteter Daten in kostengünstigere Speicherbereiche kann große Auswirkungen auf Ihr monatliches Speicherbudget und damit einhergehende Kosteneinsparungen haben. Azure bietet viele Möglichkeiten, um Ihnen bei der Identifizierung und anschließenden Speicherung dieser veralteten Daten zu helfen.

- Profitieren Sie von Zugriffsebenen für „Allgemeinen v2“-Speicher, indem Sie weniger wichtige Daten von der heißen Speicherebene zur kalten bzw. „Archiv“-Speicherebene verschieben.
- Verwenden Sie StorSimple zur Unterstützung beim Verschieben veralteter Daten, basierend auf benutzerdefinierten Richtlinien.

**Weitere Informationen** :

- Informieren Sie sich genauer zu [Zugriffsebenen](/azure/storage/blobs/storage-blob-storage-tiers).
- Lesen Sie die [Übersicht über StorSimple](/azure/azure-monitor/overview).
- Sehen Sie sich die [Preise für StorSimple](https://azure.microsoft.com/pricing/details/storsimple) an.

## <a name="best-practice-automate-vm-optimization"></a>Bewährte Methode: VM-Optimierung automatisieren

Das Hauptziel für die Ausführung einer VM in der Cloud ist die Maximierung von CPU, Arbeitsspeicher und Datenträger, die davon verwendet werden. Wenn Sie VMs ermitteln, die nicht optimiert sind, oder wenn Sie häufige Zeiträume haben, in denen VMs nicht verwendet werden, ist es sinnvoll, diese entweder herunterzufahren oder sie mithilfe von VM-Skalierungsgruppen herunterzuskalieren.

Sie können einen virtuellen Computer mit Azure Automation, VM-Skalierungsgruppen, automatischem Herunterfahren und Skript- oder Drittanbieterlösungen optimieren.

**Weitere Informationen** :

- Erfahren Sie mehr über die [vertikale automatische Skalierung](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision).
- Lesen Sie [Azure DevTest Labs: Planen des automatischen Starts von VMs](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start).
- Informieren Sie sich über das [Starten oder Beenden von VMs außerhalb von Nutzungszeiten in Azure Automation](/azure/automation/automation-solution-vm-management).
- Informieren Sie sich genauer zu [Azure Advisor](/azure/advisor/advisor-overview) und dem [Toolkit zur Azure-Ressourcenoptimierung (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-use-logic-apps-and-runbooks-with-budgets-api"></a>Bewährte Methode: Logic Apps und Runbooks mit der API für Budgets verwenden

Azure bietet eine REST-API, die Zugriff auf die Abrechnungsinformationen Ihres Mandanten hat.

- Sie können die API für Budgets verwenden, um externe Systeme und Workflows zu integrieren, die von Metriken ausgelöst werden, die Sie aus den API-Daten erstellen.
- Sie können Nutzungs- und Ressourcendaten mittels Pull in Ihre bevorzugten Datenanalysetools abrufen.
- Mithilfe der Azure-Ressourcennutzungs-API und der Azure-Ressourcen-RateCard-API können Sie Ihre Kosten genau vorhersagen und verwalten.
- Die APIs werden als Ressourcenanbieter implementiert und sind in den APIs enthalten, die von Azure Resource Manager verfügbar gemacht werden.
- Die API für Budgets kann in Azure Logic Apps und Azure Automation-Runbooks integriert werden.

**Weitere Informationen** :

- Erfahren Sie mehr über die [API für Budgets](/rest/api/consumption/budgets).
- [Gewinnen Sie Erkenntnisse](/azure/billing/billing-usage-rate-card-overview) zur Azure-Nutzung mit den Azure Abrechnungs-APIs.

## <a name="next-steps"></a>Nächste Schritte

Untersuchen Sie mit Ihren erworbenen Kenntnissen der bewährten Methoden die [Cost Management-Toolkette](./toolchain.md), um Azure-Tools und -Funktionen zu bestimmen, die Sie bei der Ausführung dieser bewährten Methoden unterstützen.

> [!div class="nextstepaction"]
> [Kostenmanagement-Toolkette für Azure](./toolchain.md)
