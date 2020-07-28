---
title: Bewerten von Windows Virtual Desktop für Azure
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich mit bewährten Methoden für die Windows Virtual Desktop-Migration vertraut zu machen, mit denen Sie die Komplexität reduzieren und den Migrationsprozess standardisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2010
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 47bcc7420cdcea5ace4397737e420434da9fd27f
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452629"
---
# <a name="windows-virtual-desktop-assessment"></a>Bewertung von Windows Virtual Desktop

Mit dem [Proof of Concept für Windows Virtual Desktop (WVD)](./proof-of-concept.md) bestimmen Sie den anfänglichen Projektumfang bzw. die Basisimplementierung. Das Ergebnis dieses Proof of Concept entspricht wahrscheinlich nicht den Produktionsanforderungen. Der Bewertungsprozess dient dazu, Annahmen mithilfe eines datengesteuerten Prozesses gezielt zu testen. Bewertungsdaten helfen Ihnen, eine Reihe wichtiger Fragen zu beantworten, die Annahmen zu validieren bzw. zu widerlegen und ggf. den Projektumfang zur Unterstützung Ihres Windows Virtual Desktop-Szenarios einzugrenzen. Dieser auf der Validierung von Annahmen beruhende Ansatz beschleunigt die Migration oder Bereitstellung von Endbenutzer-Desktops in WVD.

## <a name="assess-windows-virtual-desktop-deployments"></a>Bewerten von Windows Virtual Desktop-Bereitstellungen

Bei jeder Windows Virtual Desktop-Bewertung wird eine Kombination aus Benutzerpersona, konsistentem Hostpool (VMs), Endbenutzeranwendungen und -daten sowie Benutzerprofilen (Daten) ausgewertet. Das Ziel der Bewertung besteht darin, die Fragen in diesem Abschnitt anhand von Daten zu beantworten. Diese Antworten bestimmen den tatsächlichen Umfang der Bereitstellung und Freigabe für die WVD-Migration.

Die Voraussetzung für die Beantwortung der Fragen sind Daten. Im Rahmen der Planungsmethodik sollten insbesondere mithilfe der [bewährten Methoden](../../plan/index.md) und der [Bewertung digitaler Ressourcen](../../digital-estate/index.md) bereits Daten zum Erstellen des Migrationsplans gesammelt und analysiert worden sein. Die Fragen in dieser spezifischen Workloadbewertung erfordern jedoch wahrscheinlich zusätzliche Daten. Zum Entwickeln eines WVD-Bereitstellungsplans benötigen Sie insbesondere Daten zu den Desktops und Benutzern sowie den Workloads, die von den einzelnen Benutzern verwendet werden.

Wenn Sie das Tool [Movere](https://docs.microsoft.com/azure/migrate/migrate-services-overview#movere) zum Sammeln von Daten verwenden, verfügen Sie wahrscheinlich über die notwendigen Daten, um Personas zu entwickeln und die Fragen wie bei jedem anderen Migrationsszenario anhand von Daten in [Azure Migrate](https://docs.microsoft.com/azure/migrate) zu beantworten.

Falls Sie nicht über die erforderlichen Daten verfügen, um alle Fragen in diesem Abschnitt zu beantworten, können Sie einen separaten Ermittlungsprozess mit Software von einem Drittanbieter ausführen, um Ihre verfügbaren Daten zu ergänzen. [Lakeside](https://docs.microsoft.com/azure/migrate/migrate-services-overview#isv-integration) ist ebenfalls in Azure Migrate integriert. Das Tool ist im Abschnitt zu den Zielen der VDI-Migration verfügbar und kann zum Erstellen eines Plans für die WVD-Bereitstellung (einschließlich Personas, Hostpools, Anwendungen und Benutzerprofilen) verwendet werden.

### <a name="user-personas"></a>Benutzerpersonas

Wie viele unterschiedliche Personas sind erforderlich, um alle Benutzer im Migrationsszenario zu unterstützen? Personas werden durch die Zuordnung von Benutzern zu Buckets auf Grundlage der folgenden Daten definiert:

- **Persönliche Pools:** Sind für bestimmte Gruppen von Benutzern anstelle von Pools dedizierte Desktops erforderlich? Beispielsweise können Anforderungen im Zusammenhang mit Sicherheit, Konformität, hoher Leistung oder Beeinträchtigung durch andere Dienste („Noisy Neighbors“) dazu führen, dass einige Benutzer dedizierte Desktops verwenden, die nicht Teil einer Poolingstrategie sind. Dies wird [während der Bereitstellung des WVD-Hostpools durch die Angabe eines Hostpooltyps von Personas festgelegt](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace#begin-the-host-pool-setup-process).
- **Dichte:** Benötigen bestimmte Gruppen von Benutzern Desktopumgebungen mit geringerer Dichte? Ex. Regelmäßige Nutzer erfordern zwei Benutzer pro vCPU, während bei gelegentlichen Nutzern von sechs Benutzern pro vCPU ausgegangen wird. Dies wird in den [Pooleinstellungen der WVD-Hostpoolbereitstellung](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace#begin-the-host-pool-setup-process) eingegeben.
- **Leistung:** Benötigen bestimmte Gruppen von Benutzern Desktopumgebungen mit höherer Leistung? Ex. Manche Benutzer benötigen mehr Arbeitsspeicher pro vCPU als die angenommenen 4 GB RAM pro vCPU. Die VM-Größe wird in den [VM-Details der WVD-Hostpoolbereitstellung](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace#virtual-machine-details) eingegeben.
- **Grafikprozessor (Graphical Processing Unit, GPU):** Haben bestimmte Gruppen von Benutzern höhere Anforderungen bezüglich der Grafikleistung? Einige Benutzer benötigen beispielsweise GPU-basierte VMs in Azure (weitere Informationen finden Sie in diesem [Leitfaden zum Konfigurieren von GPU-VMs](https://docs.microsoft.com/azure/virtual-desktop/configure-vm-gpu)).
- **Azure-Region:** Arbeiten bestimmte Gruppen von Betriebssystembenutzern in verschiedenen geografischen Regionen? Vor dem Konfigurieren des Hostpools sollte ein Benutzer aus jeder Region die Wartezeit für Verbindungen mit Azure beispielsweise mit dem [Schätzungstool](https://azure.microsoft.com/services/virtual-desktop/assessment/#estimation-tool) testen. Der Testbenutzer sollte die Azure-Region mit der geringsten Wartezeit und die Wartezeit in Millisekunden für die drei wichtigsten Azure-Regionen teilen.
- **Geschäftsfunktionen:** Können die spezifischen Benutzergruppen nach Geschäftseinheit, Gebührencode oder Geschäftsfunktion Buckets zugeordnet werden? Eine solche Gruppierung ermöglicht die Anpassung der Betriebskosten in späteren Phasen.
- **Benutzeranzahl:** Wie viele Benutzer umfassen die einzelnen Personas?
- **Maximale Sitzungsanzahl:** Wie viele gleichzeitige Benutzer werden je nach Geografie und Betriebsstunden bei maximaler Auslastung für die einzelnen Personas erwartet?

Durch die mit den obigen Fragen ermittelten Unterschiede zeichnen sich erste Benutzerpersonas ab, die sich je nach **Geschäftsfunktion, Kostenstelle**, geografischer Region und technischen Anforderungen unterscheiden. Die folgende Tabelle kann Ihnen dabei helfen, die Antworten zu erfassen und ein vollständiges Bewertungs- oder Entwurfsdokument zu erstellen.

|  | Personagruppe 1  | Personagruppe 2  | Personagruppe 3  |
|---------|---------|---------|---------|
| Pools  | Pools | Pools | Dediziert (Sicherheitsaspekte) |
| Dichte | Geringe Nutzung (6 Benutzer/vCPU) | Intensive Nutzung (2 Benutzer/vCPU) | Dediziert (1 Benutzer/vCPU) |
| Leistung | Niedrig | Hohe Arbeitsspeicherauslastung | Niedrig |
| GPU | – | Erforderlich | NICHT ZUTREFFEND |
| Azure-Region | Nordamerika | Europa, Westen | Nordamerika |
| Benutzeranzahl | 1000 | 50 | 20 |
| Sitzungsanzahl | 200 | 50 | 10 |

Für jede Persona (oder Gruppe von Benutzern mit unterschiedlichen Geschäftsfunktionen), die auch individuelle technische Anforderungen hat, ist eine eigene Hostpoolkonfiguration erforderlich.

Die Endbenutzerbewertung liefert die benötigten Daten: Pooltyp, Dichte, Größe, CPU/GPU, Zielzonenregion usw.

Bei der Bewertung der Hostpoolkonfiguration werden diese Daten nun einem Bereitstellungsplan zugeordnet. Durch die Abstimmung der technischen und geschäftlichen Anforderungen sowie der Kosten können Sie die richtige Anzahl und Konfiguration der Hostpools ermitteln.

Sehen Sie sich Beispiele für die Preise in den Regionen [USA, Osten](https://azure.com/e/448606254c9a44f88798892bb8e0ef3c), [Europa, Westen](https://azure.com/e/61a376d5f5a641e8ac31d1884ade9e55) oder [Asien, Südosten](https://azure.com/e/7cf555068922461587d0aa99a476f926) an.

### <a name="application-groups"></a>Anwendungsgruppen

Die Überprüfungen der aktuellen lokalen Umgebung mithilfe von Movere und Lakeside liefern Daten zu den Anwendungen, die auf den Desktops der Endbenutzer ausgeführt werden. Erstellen Sie anhand dieser Daten eine Liste aller Anwendungen, die für die einzelnen Personas benötigt werden. Mithilfe der Antworten auf die folgenden Fragen können Sie Bereitstellungsiterationen für jede erforderliche Anwendung definieren.

- Müssen Anwendungen installiert werden, damit die Persona den Desktop verwenden kann? Sofern die Persona nicht ausschließlich webbasierte Software-as-a-Service-Anwendungen verwendet, müssen Sie wahrscheinlich für jede Persona ein [benutzerdefiniertes VHD-Masterimage](https://docs.microsoft.com/azure/virtual-desktop/set-up-customize-master-image) konfigurieren, auf dem die erforderlichen Anwendungen installiert sind.
- Benötigt diese Persona Office 365-Anwendungen? Wenn dies der Fall ist, müssen Sie [Office 365 einem angepassten VHD-Masterimage hinzufügen](https://docs.microsoft.com/azure/virtual-desktop/install-office-on-wvd-master-image).
- Ist die Anwendung kompatibel mit Windows 10 mit mehreren Sitzungen? Wenn Anwendungen nicht kompatibel sind, ist möglicherweise ein [persönlicher Pool](https://docs.microsoft.com/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) erforderlich, um das benutzerdefinierte VHD-Image auszuführen. Bei Problemen mit der Anwendungskompatibilität mit Windows Virtual Desktop kann Ihnen auch der Dienst [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-app-assure-assistance-offered) weiterhelfen.
- Werden unternehmenskritische Anwendungen voraussichtlich unter der Wartezeit zwischen dem virtuellen Desktop und Back-End-Systemen leiden? Wenn dies der Fall ist, sollten Sie die Back-End-Systeme, die die Anwendung unterstützen, ggf. zu Azure migrieren.

Die Antworten auf diese Fragen erfordern möglicherweise, dass die Wartung der Desktopimages oder unterstützenden Anwendungskomponenten schon vor der Desktopmigration oder -bereitstellung im Plan berücksichtigt werden.

## <a name="next-step-deploy-or-migrate-windows-virtual-desktop-instances"></a>Nächster Schritt: Bereitstellen oder Migrieren von Windows Virtual Desktop-Instanzen

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Migrieren oder Bereitstellen von Windows Virtual Desktop-Instanzen](./migrate-deploy.md)
- [Veröffentlichen der Windows Virtual Desktop-Bereitstellung in der Produktionsumgebung](./migrate-release.md)
