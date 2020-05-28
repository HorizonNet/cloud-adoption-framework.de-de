---
title: Wie funktioniert Azure?
description: Hier finden Sie grundlegende Informationen zur internen Struktur und zur Funktionsweise der Azure-Cloudplattform und der Cloudvirtualisierung.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 00d5709aeb0a922b8f8c5efd26abafe70d70a237
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755159"
---
<!-- cSpell:ignore PDU -->

<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Wie funktioniert Azure?

Azure ist die öffentliche Cloudplattform von Microsoft. Azure umfasst eine große Sammlung von Diensten, z. B. PaaS- (Platform as a Service), IaaS- (Infrastructure-as-a-Service) und verwaltete Datenbankdienste. Aber was ist Azure genau, und wie funktioniert es?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2ixGo]

Wie andere Cloudplattformen auch, basiert Azure auf einer Technologie, die als _Virtualisierung_ bezeichnet wird. Ein Großteil der Computerhardware kann per Software emuliert werden, da es sich bei Computerhardware in den meisten Fällen lediglich um einen Satz mit Anweisungen handelt, die permanent oder semipermanent in Silizium codiert sind. Indem eine Emulationsebene verwendet wird, mit der Softwareanweisungen Hardwareanweisungen zugeordnet werden, kann virtualisierte Hardware so per Software ausgeführt werden, als ob es sich wirklich um Hardware handeln würde.

Im Wesentlichen umfasst die Cloud eine Gruppe von physischen Servern in einem oder mehreren Rechenzentren, auf denen virtualisierte Hardware im Namen der Kunden ausgeführt wird. Wie wird es also für die Cloud erreicht, dass Millionen von Instanzen virtualisierter Hardware für Millionen von Kunden gleichzeitig erstellt, gestartet, beendet und gelöscht werden können?

Wir sehen uns die Architektur der Hardware im Rechenzentrum an. Jedes Rechenzentrum verfügt über eine Sammlung von Servern, die in Serverracks angeordnet sind. Jedes Serverrack enthält viele Server**blades** sowie einen Netzwerkswitch für die Netzwerkkonnektivität und eine Stromversorgungseinheit für die Stromversorgung. Racks werden auch in größeren Einheiten gruppiert, die als _Cluster_ bezeichnet werden.

Innerhalb jedes Racks oder Clusters haben die meisten Server die Aufgabe, diese virtualisierten Hardwareinstanzen im Namen des Benutzers auszuführen. Auf einigen Servern wird jedoch Software für die Cloudverwaltung ausgeführt, die als Fabric Controller bezeichnet wird. Der _Fabric Controller_ ist eine verteilte Anwendung mit vielen Aufgaben. Er dient zum Zuordnen von Diensten, Überwachen der Integrität des Servers und der darauf ausgeführten Dienste und Wiederherstellen der Serverintegrität nach einem Ausfall.

Jede Instanz des Fabric Controllers ist mit einem anderen Satz von Servern verbunden, auf denen Software für die Cloudorchestrierung ausgeführt wird, die normalerweise als _Front-End_ bezeichnet wird. Auf dem Front-End werden die Webdienste, RESTful-APIs und internen Azure-Datenbanken gehostet, die für alle Funktionen der Cloud verwendet werden.

Beispielsweise hostet das Front-End die Dienste, mit denen Kundenanforderungen zur Zuteilung von Azure-Ressourcen verarbeitet werden. Hierzu zählen beispielsweise [virtuelle Computer](https://docs.microsoft.com/azure/virtual-machines) (VMs) und Dienste wie [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Zuerst überprüft das Front-End den Benutzer und stellt sicher, dass der Benutzer zur Zuordnung der angeforderten Ressourcen berechtigt ist. Falls ja, zieht das Front-End eine Datenbank heran, um ein Serverrack mit ausreichender Kapazität zu ermitteln. Anschließend weist es den Fabric Controller im Rack an, die Ressource zuzuteilen.

Azure ist also im Wesentlichen eine riesige Sammlung von Servern und Netzwerkhardware-Komponenten, auf denen ein komplexer Satz verteilter Anwendungen ausgeführt wird, um Konfiguration und Betrieb der virtualisierten Hardware und Software auf diesen Servern zu orchestrieren. Diese Orchestrierung macht Azure so leistungsstark. Benutzer müssen sich nicht mehr um die Wartung und Upgrades von Hardware kümmern, da diese Aufgaben von Azure im Hintergrund durchgeführt werden.

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Cloudeinführung per [Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework)](../index.yml).

> [!div class="nextstepaction"]
> [Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework)](../index.yml)
