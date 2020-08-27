---
title: Bewerten von Windows Virtual Desktop für Azure
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität reduzieren und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d313641025bd5cc768c3e4f99feedb768880f396
ms.sourcegitcommit: 8b5fdb68127c24133429b4288f6bf9004a1d1253
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88848277"
---
# <a name="windows-virtual-desktop-assessment"></a>Bewertung von Windows Virtual Desktop

Mit dem [Proof of Concept für Windows Virtual Desktop (WVD)](./proof-of-concept.md) liefert den anfänglichen Projektumfang bzw. die Basisimplementierung für das Contoso-Cloudeinführungsteam. Das Ergebnis dieses Proof of Concept entspricht jedoch wahrscheinlich nicht den Produktionsanforderungen.

Der Windows Virtual Desktop-Bewertungsübung dient dazu, Annahmen mithilfe eines datengesteuerten Prozesses gezielt zu testen. Bewertungsdaten helfen dem Team dabei, eine Reihe wichtiger Fragen zu beantworten, die Annahmen zu belegen oder zu widerlegen und ggf. den Projektumfang zugunsten des Windows Virtual Desktop-Szenarios des Teams einzugrenzen. Mit diesem auf der Validierung von Annahmen beruhenden Ansatz kann das Team die Migration oder Bereitstellung von Endbenutzerdesktops in Windows Virtual Desktop beschleunigen.

## <a name="assess-windows-virtual-desktop-deployments"></a>Bewerten von Windows Virtual Desktop-Bereitstellungen

Bei jeder Windows Virtual Desktop-Bewertung wird eine Kombination aus Benutzerpersona, konsistentem Hostpool der virtuellen Computer (VMs), Endbenutzeranwendungen und -daten sowie Benutzerprofilen (Daten) ausgewertet. Das Team verfolgt mit der Bewertung das Ziel, die Fragen in diesem Abschnitt anhand von Daten zu beantworten. Diese Antworten bestimmen den tatsächlichen Umfang der Bereitstellung und Freigabe für die Windows Virtual Desktop-Migration.

Die Voraussetzung für die Beantwortung der Fragen sind Daten. Im Rahmen der Planungsmethodik sollten insbesondere mithilfe der [bewährten Methoden](../../plan/index.md) und der [Bewertung digitaler Ressourcen](../../digital-estate/index.md) bereits Daten zum Erstellen eines Migrationsplans gesammelt und analysiert worden sein. Die Fragen in dieser spezifischen Workloadbewertung erfordern jedoch wahrscheinlich zusätzliche Daten. Zum Entwickeln eines Windows Virtual Desktop-Bereitstellungsplans benötigen Sie Daten zu den Desktops und Benutzern sowie den Workloads, die von den einzelnen Benutzern verwendet werden.

Wenn Sie das Tool [Movere](/azure/migrate/migrate-services-overview#movere) zum Sammeln von Daten verwenden, verfügen Sie wahrscheinlich über die notwendigen Daten, um Personas zu entwickeln und die Fragen wie bei jedem anderen Migrationsszenario anhand von Daten in [Azure Migrate](/azure/migrate) zu beantworten.

Falls Sie nicht über die erforderlichen Daten verfügen, um alle Fragen in diesem Abschnitt zu beantworten, können Sie diese in einem separaten Ermittlungsprozess mit Software von einem Drittanbieter ergänzen. Der Hersteller [Lakeside](/azure/migrate/migrate-services-overview#isv-integration) ist auch mit Azure Migrate im Abschnitt zu Migrationszielen für virtuelle Desktopinfrastruktur integriert. Der Hersteller kann Ihnen bei der Ausarbeitung eines Plans für die Windows Virtual Desktop-Bereitstellung (einschließlich Personas, Hostpools, Anwendungen und Benutzerprofilen) helfen.

### <a name="user-personas"></a>Benutzerpersonas

Wie viele unterschiedliche Personas sind erforderlich, um alle Benutzer im Migrationsszenario zu unterstützen? Personas werden durch die Zuordnung von Benutzern zu Buckets auf Grundlage der folgenden Kriterien definiert:

- **Persönliche Pools:** Sind für bestimmte Benutzergruppen dedizierte Desktops anstelle von Pools erforderlich? Beispielsweise können Anforderungen im Zusammenhang mit Sicherheit, Konformität, hoher Leistung oder Beeinträchtigung durch andere Dienste („Noisy Neighbors“) dazu führen, dass einige Benutzer dedizierte Desktops verwenden, die nicht Teil einer Poolingstrategie sind. Sie geben diese Informationen ein, indem Sie während der [Bereitstellung des Windows Virtual Desktop-Hostpools den Hostpooltyp „Persönlich“ festlegen](/azure/virtual-desktop/create-host-pools-azure-marketplace#begin-the-host-pool-setup-process).
- **Dichte:** Benötigen bestimmte Benutzergruppen Desktopumgebungen mit geringerer Dichte? Beispielsweise lässt die größere Dichte möglicherweise nur zwei Benutzer pro vCPU (Virtual Central Processing Unit) anstelle der Annahme von sechs Benutzern pro vCPU bei niedrigerer Dichte zu. Sie geben die Dichteinformationen in den [Pooleinstellungen der Windows Virtual Desktop-Hostpoolbereitstellung](/azure/virtual-desktop/create-host-pools-azure-marketplace#begin-the-host-pool-setup-process) an.
- **Leistung**: Benötigen bestimmte Benutzergruppen Desktopumgebungen mit höherer Leistung? Manche Benutzer benötigen beispielsweise mehr Arbeitsspeicher pro vCPU als die angenommenen 4&nbsp;GB RAM pro vCPU. Sie geben die VM-Größe in den [VM-Details der Windows Virtual Desktop-Hostpoolbereitstellung](/azure/virtual-desktop/create-host-pools-azure-marketplace#virtual-machine-details) ein.
- **Grafikprozessor (Graphical Processing Unit, GPU):** Haben bestimmte Benutzergruppen höhere Anforderungen bezüglich der Grafikleistung? Einige Benutzer benötigen beispielsweise GPU-basierte VMs in Azure (weitere Informationen finden Sie in diesem [Leitfaden zum Konfigurieren von GPU-VMs](/azure/virtual-desktop/configure-vm-gpu)).
- **Azure-Region:** Arbeiten bestimmte Gruppen von Betriebssystembenutzern in verschiedenen geografischen Regionen? Vor dem Konfigurieren des Hostpools sollte ein Benutzer aus jeder Region die Latenz für Verbindungen mit Azure beispielsweise mit dem [Schätzungstool](https://azure.microsoft.com/services/virtual-desktop/assessment/#estimation-tool) testen. Der Testbenutzer sollte die Azure-Region mit der geringsten Latenz und die Latenz in Millisekunden für die drei wichtigsten Azure-Regionen teilen.
- **Geschäftsfunktionen:** Können die spezifischen Benutzergruppen nach Geschäftseinheit, Gebührencode oder Geschäftsfunktion Buckets zugeordnet werden? Eine solche Gruppierung ermöglicht die Anpassung der Betriebskosten in späteren Phasen.
- **Benutzeranzahl:** Wie viele Benutzer umfassen die einzelnen Personas?
- **Maximale Sitzungsanzahl:** Wie viele gleichzeitige Benutzer werden je nach Geografie und Betriebsstunden bei maximaler Auslastung für die einzelnen Personas erwartet?

Durch die mit den vorherigen Fragen ermittelten Unterschiede zeichnen sich erste Benutzerpersonas ab, die sich je nach Geschäftsfunktion, Kostenstelle, geografischer Region und technischen Anforderungen unterscheiden. Die folgende Tabelle kann Ihnen dabei helfen, die Antworten zu erfassen und ein vollständiges Bewertungs- oder Entwurfsdokument zu erstellen:

| Kriterium  | Personagruppe&nbsp;1  | Personagruppe&nbsp;2  | Personagruppe&nbsp;3  |
|---------|---------|---------|---------|
| Pools  | Pools | Pools | Dediziert (Sicherheitsaspekte) |
| Dichte | Niedrig (6&nbsp;Benutzer/vCPU) | Hoch (2&nbsp;Benutzer/vCPU) | Dediziert (1&nbsp;Benutzer/vCPU) |
| Leistung | Niedrig | Hohe Arbeitsspeicherauslastung | Niedrig |
| GPU | – | Erforderlich | NICHT ZUTREFFEND |
| Azure-Region | Nordamerika | Europa, Westen | Nordamerika |
| Benutzeranzahl | 1000 | 50 | 20 |
| Sitzungsanzahl | 200 | 50 | 10 |

Für jede Persona oder Benutzergruppe mit unterschiedlichen Geschäftsfunktionen und technischen Anforderungen ist eine eigene Hostpoolkonfiguration erforderlich.

Die Endbenutzerbewertung liefert die erforderlichen Daten: Pooltyp, Dichte, Größe, CPU/GPU, Zielzonenregion usw.

Bei der Bewertung der Hostpoolkonfiguration werden diese Daten nun einem Bereitstellungsplan zugeordnet. Durch die Abstimmung der technischen und geschäftlichen Anforderungen sowie der Kosten können Sie die richtige Anzahl und Konfiguration für Hostpools ermitteln.

Sehen Sie sich Beispiele für die Preise in den Regionen [USA, Osten](https://azure.com/e/448606254c9a44f88798892bb8e0ef3c), [Europa, Westen](https://azure.com/e/61a376d5f5a641e8ac31d1884ade9e55) oder [Asien, Südosten](https://azure.com/e/7cf555068922461587d0aa99a476f926) an.

### <a name="application-groups"></a>Anwendungsgruppen

Die Überprüfungen der aktuellen lokalen Umgebung mithilfe von Movere und Lakeside liefern Daten zu den Anwendungen, die auf den Desktops der Endbenutzer ausgeführt werden. Anhand dieser Daten können Sie eine Liste aller Anwendungen erstellen, die für die einzelnen Personas benötigt werden. Mithilfe der Antworten auf die folgenden Fragen können Sie Bereitstellungsiterationen für jede erforderliche Anwendung definieren:

- Müssen Anwendungen installiert werden, damit die Persona den Desktop verwenden kann? Sofern die Persona nicht ausschließlich webbasierte Software-as-a-Service-Anwendungen verwendet, müssen Sie wahrscheinlich für jede Persona ein [benutzerdefiniertes VHD-Masterimage](/azure/virtual-desktop/set-up-customize-master-image) konfigurieren, auf dem die erforderlichen Anwendungen installiert sind.
- Benötigt diese Persona Microsoft 365-Anwendungen? Wenn das der Fall ist, müssen Sie [Microsoft 365 einem angepassten VHD-Masterimage hinzufügen](/azure/virtual-desktop/install-office-on-wvd-master-image).
- Ist die Anwendung mit Windows&nbsp;10 mit mehreren Sitzungen kompatibel? Wenn eine Anwendung nicht kompatibel ist, ist möglicherweise ein [persönlicher Pool](/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) erforderlich, um das benutzerdefinierte VHD-Image auszuführen. Der Dienst [Desktop App Assure](/fasttrack/win-10-app-assure-assistance-offered) bietet Unterstützung bei Problemen mit der Kompatibilität von Anwendungen und Windows Virtual Desktop.
- Werden unternehmenskritische Anwendungen voraussichtlich von der Latenz zwischen dem der Windows Virtual Desktop-Instanz und den Back-End-Systemen beeinträchtigt? Wenn das der Fall ist, sollten Sie die Back-End-Systeme, die die Anwendung unterstützen, ggf. zu Azure migrieren.

Die Antworten auf diese Fragen setzen möglicherweise voraus, dass die Wartung der Desktopimages oder unterstützenden Anwendungskomponenten schon vor der Desktopmigration oder -bereitstellung im Plan berücksichtigt wird.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
