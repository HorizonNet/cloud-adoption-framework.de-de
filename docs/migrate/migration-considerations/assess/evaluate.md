---
title: Bewerten der Bereitschaft einer Workload
description: Ein Prozess innerhalb der Cloudmigration, der sich auf die Aufgaben der Migration von Workloads in die Cloud konzentriert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c695d83c4e04b3cd837ff5916e47c128f17a1d34
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802547"
---
# <a name="evaluate-workload-readiness"></a>Bewerten der Bereitschaft einer Workload

Diese Aktivität konzentriert sich auf das Bewerten der Bereitschaft einer Workload für die Migration in die Cloud. Während dieser Aktivität überprüft das Cloudeinführungsteam, ob alle Ressourcen und zugehörigen Abhängigkeiten mit dem gewählten Bereitstellungsmodell und Cloudanbieter kompatibel sind. Während des Prozesses dokumentiert das Team alle Maßnahmen, die zum [Beheben](../migrate/remediate.md) von Kompatibilitätsproblemen erforderlich sind.

## <a name="evaluation-assumptions"></a>Annahmen zur Bewertung

Der Großteil des Inhalts, der Prinzipien im Framework für die Cloudeinführung zum Thema hat, ist cloudunabhängig gehalten. Der Prozess zum Bewerten der Bereitschaft jedoch muss weitgehend spezifisch für die jeweilige Cloudplattform sein. Bei den folgenden Anleitungen wird von einer Migration nach Azure ausgegangen. Außerdem wird die Verwendung von Azure Migrate (auch bekannt als Azure Site Recovery) für [Replikationsaktivitäten](../migrate/replicate.md) vorausgesetzt. Informationen zu alternativen Tools finden Sie unter [Replikationsoptionen](../migrate/replicate-options.md).

Dieser Artikel ist keine Auflistung aller möglichen Bewertungsaktivitäten. Es wird davon ausgegangen, dass jede Umgebung und jedes Geschäftsergebnis spezifische Anforderungen stellt. Um die Aufstellung dieser Anforderungen zu beschleunigen, sind im restlichen Teil dieses Artikels einige allgemeine Bewertungsaktivitäten im Zusammenhang mit der Bewertung von [Infrastruktur](#common-infrastructure-evaluation-activities), [Datenbank](#common-database-evaluation-activities) und [Netzwerk](#common-network-evaluation-activities) aufgeführt.

## <a name="common-infrastructure-evaluation-activities"></a>Allgemeine Bewertungsaktivitäten für die Infrastruktur

- VMware-Anforderungen: [Überprüfen Sie die Azure Site Recovery-Anforderungen für VMware](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix).
- Hyper-V-Anforderungen: [Überprüfen Sie die Azure Site Recovery-Anforderungen für Hyper-V](https://docs.microsoft.com/azure/site-recovery/hyper-v-azure-support-matrix).

Achten Sie darauf, alle Abweichungen bei der Hostkonfiguration, der replizierten VM-Konfiguration, dem Speicherbedarf oder der Netzwerkkonfiguration zu dokumentieren.

## <a name="common-database-evaluation-activities"></a>Allgemeine Bewertungsaktivitäten für Datenbanken

- Dokumentieren Sie die Recovery Point Objectives (RPO) und Recovery Time Objectives (RTO) der aktuellen Datenbankbereitstellung. Diese werden bei [Architekturaktivitäten](./architect.md) als Hilfe zur Entscheidungsfindung verwendet.
- Dokumentieren Sie alle Anforderungen für die Hochverfügbarkeitskonfiguration. Informationen zum Verständnis der SQL Server-Anforderungen finden Sie im [Leitfaden zu SQL Server-Lösungen mit hoher Verfügbarkeit](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).
- Bewerten Sie die PaaS-Kompatibilität. Im [Leitfaden für die Azure-Datenmigration](https://datamigration.microsoft.com) werden lokale Datenbanken den kompatiblen Azure-PaaS-Lösungen zugeordnet, z. B. [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) oder [Azure DB](https://docs.microsoft.com/azure/sql-database) für [MySQL](https://docs.microsoft.com/azure/mysql), [PostgreSQL](https://docs.microsoft.com/azure/postgresql) oder [MariaDB](https://docs.microsoft.com/azure/mariadb).
- Wenn PaaS-Kompatibilität möglich ist, ohne dass eine Problembehandlung erforderlich ist, wenden Sie sich an das für [Architekturaktivitäten](./architect.md) verantwortliche Team. PaaS-Migrationen können bei den meisten Cloudlösungen zu erheblichen Zeiteinsparungen und Reduzierungen der Gesamtbetriebskosten führen.
- Wenn PaaS-Kompatibilität möglich ist, jedoch eine Problembehandlung erforderlich ist, wenden Sie sich an die für [Architekturaktivitäten](./architect.md) und [Problembehandlungsaktivitäten](../migrate/remediate.md) verantwortlichen Teams. In vielen Szenarien können die Vorteile von PaaS-Migrationen für Datenbanklösungen die längere Problembehandlungszeit aufwiegen.
- Dokumentieren Sie Änderungsumfang und -rate für jede zu migrierende Datenbank.
- Dokumentieren Sie möglichst alle Anwendungen oder anderen Ressourcen, die Aufrufe der einzelnen Datenbanken durchführen.

> [!NOTE]
> Die Synchronisierung einer Ressource belegt Bandbreite während der Replikationsprozesse. Eine sehr häufiger Fehler ist es, den Bandbreitenbedarf zu übersehen, der erforderlich ist, um Ressourcen zwischen dem Zeitpunkt der Replikation und der Freigabe synchron zu halten. Datenbanken belegen häufig Bandbreite während der Releasezyklen. Dies ist insbesondere bei Datenbanken mit hohem Speicherbedarf oder hoher Änderungsrate der Fall. Erwägen Sie einen Ansatz zur Replikation der Datenstruktur mit gesteuerten Updates vor Benutzerakzeptanztest (UAT) und Freigabe. In solchen Szenarien sind Alternativen zu Azure Site Recovery möglicherweise besser geeignet. Weitere Informationen finden Sie in den Anleitungen im [Leitfaden für die Azure-Datenmigration](https://datamigration.microsoft.com).

## <a name="common-network-evaluation-activities"></a>Allgemeine Bewertungsaktivitäten für das Netzwerk

- Berechnen Sie den Gesamtspeicher für alle virtuellen Computer, die während der Iterationen bis zu einem Release repliziert werden sollen.
- Berechnen Sie die Abweichung oder Änderungsrate des Speichers für alle virtuellen Computer, die während der Iterationen bis zu einem Release repliziert werden sollen.
- Berechnen Sie den erforderlichen Bandbreitenbedarf für jede Iteration durch Summieren von Gesamtspeicher und Abweichung.
- Berechnen Sie die ungenutzte Bandbreite, die im aktuellen Netzwerk verfügbar ist, um die Ausrichtung pro Iteration zu überprüfen.
- Dokumentieren Sie die Bandbreite, die benötigt wird, um die erwartete Migrationsgeschwindigkeit zu erreichen. Wenn eine Problembehandlung erforderlich ist, um die erforderliche Bandbreite bereitzustellen, benachrichtigen Sie das für [Problembehandlungsaktivitäten](../migrate/remediate.md) verantwortliche Team.

> [!NOTE]
> Der Gesamtspeicher wirkt sich direkt auf den Bandbreitenbedarf während der ersten Replikation aus. Die Speicherabweichung setzt sich jedoch vom Zeitpunkt der Replikation bis zur Freigabe fort. Das bedeutet, dass die Abweichung eine kumulative Auswirkung auf die verfügbare Bandbreite hat.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die Bewertung eines Systems abgeschlossen ist, fließen die Ergebnisse in die Entwicklung einer neuen [Cloudarchitektur](./architect.md) ein.

> [!div class="nextstepaction"]
> [Entwerfen von Workloads vor der Migration](./architect.md)
