---
title: Genehmigen von Änderungen an der Architektur vor der Migration
description: Es wird beschrieben, wie Sie die Änderungen an der Architektur klassifizieren, wenn diese erforderlich sind, und geeignete Genehmigungsaktivitäten einrichten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d59f2d92f6777cd3210de715eb0de217fe9abce8
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80432914"
---
<!-- cSpell:ignore architected ITIL -->

# <a name="approve-architecture-changes-before-migration"></a>Genehmigen von Änderungen an der Architektur vor der Migration

Während des Bewertungsprozesses der Migration wird jede Workload beurteilt, entworfen und geschätzt, um einen Plan für den zukünftigen Zustand der Workload zu entwickeln. Einige Workloads können ohne Änderung der Architektur in die Cloud migriert werden. Durch Beibehaltung der lokalen Konfiguration und Architektur kann das Risiko reduziert und der Migrationsprozess optimiert werden. Leider kann nicht jede Anwendung ohne Änderung der Architektur in der Cloud ausgeführt werden. Wenn Architekturänderungen erforderlich sind, kann dieser Artikel beim Klassifizieren der Änderung helfen. Außerdem enthält er hilfreiche Informationen zu den geeigneten Genehmigungsaktivitäten.

## <a name="business-impact-and-approval"></a>Geschäftliche Auswirkungen und Genehmigung

Während der Migration ergeben sich wahrscheinlich Änderungen, die sich auch auf das Geschäft auswirken. Zwar lassen sich Änderungen manchmal nicht vermeiden, doch sollte es keine Überraschungen aufgrund nicht offengelegter oder nicht dokumentierter Änderungen geben. Um die Unterstützung der Beteiligten während der gesamten Migration aufrechtzuerhalten, ist es wichtig, Überraschungen zu vermeiden. Überraschungen für Anwendungsbesitzer oder Beteiligte im Unternehmen können eine Cloudeinführung verlangsamen oder stoppen.

Vor der Migration ist es wichtig, den geschäftlichen Besitzer der Workload auf Änderungen vorzubereiten, die sich auf Geschäftsprozesse auswirken können. Dazu gehören z. B. Änderungen in Bezug auf Folgendes:

- Vereinbarungen zum Servicelevel
- Zugriffsmuster oder Sicherheitsanforderungen, die sich auf den Endbenutzer auswirken
- Datenaufbewahrungsmethoden
- Kernanwendungsleistung

Selbst wenn eine Workload mit minimaler bis gar keiner Änderung migriert werden kann, sind dennoch geschäftliche Auswirkungen möglich. Replikationsprozesse können die Leistung von Produktionssystemen verlangsamen. Änderungen an der Umgebung zur Vorbereitung auf die Migration können möglicherweise zu Einschränkungen der Routing- oder Netzwerkleistung führen. Es gibt eine Vielzahl weiterer Auswirkungen, die sich durch Replikations-, Staging- oder Höherstufungsaktivitäten ergeben können.

Regelmäßige Genehmigungsaktivitäten können dazu beitragen, Überraschungen aufgrund von Änderungen oder leistungsbedingten Geschäftsauswirkungen zu minimieren oder zu vermeiden. Das Cloudeinführungsteam sollte am Ende des Bewertungsprozesses und vor Beginn des Migrationsprozesses einen Änderungsgenehmigungsprozess durchführen.

## <a name="existing-culture"></a>Vorhandene Kultur

Ihre IT-Teams verfügen wahrscheinlich über bestehende Mechanismen zur Verwaltung von Änderungen im Zusammenhang mit Ihren lokalen Ressourcen. Diese Mechanismen werden in der Regel durch herkömmliche Change Management-Prozesse gesteuert, die auf ITIL (Information Technology Infrastructure Library) basieren. Bei vielen Unternehmensmigrationen beinhalten diese Prozesse ein Change Advisory Board (CAB), das für die Überprüfung, Dokumentation und Genehmigung aller IT-bezogenen Änderungsanforderungen zuständig ist.

Das CAB besteht in der Regel aus Experten aus mehreren IT- und betriebswirtschaftlichen Teams und bietet eine Vielzahl von Perspektiven sowie eine detaillierte Überprüfung aller IT-bezogenen Änderungen. Ein CAB-Genehmigungsprozess ist eine bewährte Methode, um Risiken zu reduzieren und die geschäftlichen Auswirkungen von Änderungen unter Einbeziehung stabiler, durch IT-Vorgänge verwalteter Workloads zu minimieren.

## <a name="technical-approval"></a>Technische Genehmigung

Die Bereitschaft der Organisation zur Genehmigung technischer Änderungen gehört zu den häufigsten Gründen für das Scheitern der Cloudmigration. Es werden mehr Projekte durch eine Reihe technischer Genehmigungen blockiert als durch jede andere Schwachstelle in einer Cloudplattform. Das Vorbereiten der Organisation auf die Genehmigung technischer Änderungen ist eine wichtige Voraussetzung für den Erfolg der Migration. Es folgen einige bewährte Methoden, um sicherzustellen, dass die Organisation für technische Genehmigungen bereit ist.

### <a name="itil-change-advisory-board-challenges"></a>Herausforderungen für ITIL und Change Advisory Board

Jede Change Management-Methode hat ihre eigenen Steuerelemente und Genehmigungsprozesse. Die Migration ist eine Reihe von kontinuierlichen Änderungen, die mit einem hohen Maß an Unklarheit beginnen und im Laufe der Ausführung größere Klarheit entwickeln. Daher wird die Migration am besten durch agilitätsbasierte Change Management-Ansätze gesteuert, wobei das Cloudstrategieteam als Produktbesitzer fungiert.

Der Umfang und die Häufigkeit von Änderungen während einer Cloudmigration passen jedoch nicht gut zu ITIL-Prozessen. Die Anforderungen einer CAB-Genehmigung können den Erfolg einer Migration gefährden und die Maßnahme verlangsamen oder stoppen. Darüber hinaus ist in den frühen Phasen der Migration die Unklarheit groß und die Fachkenntnis eher gering. Bei den ersten paar Workloadmigrationen oder -freigaben befindet sich das Cloudeinführungsteam oft noch in der Lernphase. Daher kann es für das Team schwierig sein, die Datentypen bereitzustellen, die für eine erfolgreiche CAB-Genehmigung erforderlich sind.

Die folgenden bewährten Methoden können dem CAB helfen, während der Migration ein gewisses Maß an Komfort aufrechtzuerhalten, ohne zu einem beschwerlichen Hindernis zu werden.

### <a name="standardize-change"></a>Standardisieren der Änderung

Es ist verlockend für ein Cloudeinführungsteam, detaillierte Architekturentscheidungen für jede Workload zu treffen, die in die Cloud migriert wird. Es ist ebenso verlockend, eine Cloudmigration als Katalysator zur Umgestaltung früherer Architekturentscheidungen zu nutzen. Bei Organisationen, die ein paar Hundert virtuelle Computer oder ein paar Dutzend Workloads migrieren, können beide Ansätze entsprechend verwaltet werden. Bei der Migration eines Rechenzentrums, das aus 1.000 oder mehr Ressourcen besteht, wird jeder dieser Ansätze als ein risikoreiches Antimuster betrachtet, das die Erfolgswahrscheinlichkeit deutlich reduziert. Modernisierung, Umgestaltung und Umstrukturierung jeder Anwendung erfordern unterschiedlichste Fähigkeiten und eine Vielzahl von Änderungen, und diese Aufgaben schaffen Abhängigkeiten von menschlichen Tätigkeiten in entsprechendem Umfang. Jede dieser Abhängigkeiten birgt ein Risiko für die Migration.

Im Artikel zur [Rationalisierung digitaler Ressourcen](../../../digital-estate/rationalize.md) wird die Agilität und der zeitsparende Einfluss von grundlegenden Annahmen bei der Rationalisierung digitaler Ressourcen erläutert. Standardisierte Änderungen haben einen weiteren Vorteil. Durch Auswahl eines standardmäßigen Rationalisierungsansatzes zur Steuerung der Migrationsmaßnahme kann das Cloud Advisory Board oder der Produktbesitzer die Anwendung einer einzigen Änderung für eine langen Liste von Workloads überprüfen und genehmigen. Dadurch wird die technische Genehmigung einzelner Workloads auf solche reduziert, bei denen für Kompatibilität mit der Cloud eine erhebliche Architekturänderung erforderlich ist.

### <a name="clarify-expectations-and-roles-of-approvers"></a>Verdeutlichen von Erwartungen und Rollen der genehmigenden Personen

Vor der Bewertung der ersten Workload sollte das Cloudstrategieteam die Erwartungen jeder Person, die an der Genehmigung von Änderungen beteiligt ist, dokumentieren und kommunizieren. Durch diese einfache Aktivität können kostspielige Verzögerungen vermieden werden, wenn das Cloudeinführungsteam vollständig eingebunden ist.

### <a name="seek-approval-early"></a>Frühzeitiges Einholen der Genehmigung

Wenn möglich, sollten technische Änderungen während des Bewertungsprozesses erkannt und dokumentiert werden. Unabhängig von den Genehmigungsprozessen sollte das Cloudeinführungsteam die genehmigenden Personen frühzeitig einbinden. Je früher die Änderungsgenehmigung beginnen kann, desto unwahrscheinlicher ist es, dass ein Genehmigungsprozess die Migrationsaktivitäten blockiert.

## <a name="next-steps"></a>Nächste Schritte

Mithilfe dieser bewährten Methoden sollte es einfacher sein, eine ordnungsgemäße und risikoarme Genehmigung in die Migrationsmaßnahmen zu integrieren. Nachdem die Änderungen der Workloads genehmigt wurden, ist das Cloudeinführungsteam zum [Migrieren von Workloads](../migrate/index.md) bereit.

> [!div class="nextstepaction"]
> [Migrieren von Workloads](../migrate/index.md)
