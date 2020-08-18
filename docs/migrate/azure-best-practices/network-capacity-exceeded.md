---
title: Bewährte Methoden bei Überschreitung der Netzwerkkapazität durch Datenanforderungen während einer Migration
description: Bewährte Methoden bei Überschreitung der Netzwerkkapazität durch Datenanforderungen während einer Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 28a06749f9681f42ede11813c1477754418236b1
ms.sourcegitcommit: 452e09b543e7b84f943db5b02480ba2d18afd939
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87866212"
---
<!-- cSpell:ignore HDFS databox VHDX -->

# <a name="best-practices-when-data-requirements-exceed-network-capacity-during-a-migration-effort"></a>Bewährte Methoden bei Überschreitung der Netzwerkkapazität durch Datenanforderungen während einer Migration

Bei einer Cloudmigration werden Ressourcen über das Netzwerk zwischen dem vorhandenen Rechenzentrum und der Cloud repliziert und synchronisiert. Es ist nicht ungewöhnlich, dass die vorhandenen Datengrößenanforderungen von verschiedenen Workloads die Netzwerkkapazität übersteigen. In einem solchen Szenario kann der Migrationsprozess sich drastisch verlangsamen oder in einigen Fällen ganz beendet werden. Die folgende Anleitung ergänzt den [Azure-Migrationsleitfaden](../azure-migration-guide/index.md) um eine Lösung zur Umgehung von Netzwerkeinschränkungen.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die meisten dieser Ergänzungen beziehen sich auf die Voraussetzungen sowie die Bewertungs- und Migrationsphase einer Migration.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

**Überprüfen von Risiken der Netzwerkkapazität:** Die [Rationalisierung digitaler Ressourcen](../../digital-estate/rationalize.md) ist eine dringend empfohlene Voraussetzung, insbesondere was die Problematik der Überlastung der verfügbaren Netzwerkkapazität angeht. Bei der Rationalisierung digitaler Ressourcen erfassen Sie einen [Bestand digitaler Ressourcen](../../digital-estate/inventory.md). Dieser Bestand sollte die vorhandenen Speicheranforderungen für die digitalen Ressourcen enthalten. 

Wie unter [Replikationsrisiken – Physikalische Grundlagen der Replikation](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) beschrieben, können Sie anhand dieses Bestands die Gesamtgröße der Migrationsdaten schätzen und mit der für die Migration verfügbaren Gesamtbandbreite vergleichen. Wenn dieser Vergleich nicht mit der erforderlichen Zeit bis zur Geschäftsänderung übereinstimmt, kann dieser Artikel Ihnen helfen, die Migrationsgeschwindigkeit zu beschleunigen und die für die Migration des Rechenzentrums erforderliche Zeit zu verringern.

**Offlineübertragung von unabhängigen Datenspeichern:** In der folgenden Abbildung sind Beispiele für die Onlinedatenübertragung sowie die Offlinedatenübertragung mit Azure Data Box dargestellt. Diese Ansätze können verwendet werden, um große Datenmengen vor der Workloadmigration in die Cloud zu versenden. Bei einer Offlinedatenübertragung kopieren Sie die Quelldaten auf den Azure Data Box-Datenträger, der dann zur Übertragung der Daten in ein Azure Storage-Konto als Datei oder Blob physisch an Microsoft gesendet wird. Bevor Sie andere Migrationsansätze verfolgen, können Sie so Daten versenden, die nicht direkt an eine bestimmte Workload gebunden sind. Dadurch wird die Menge der Daten reduziert, die über das Netzwerk übertragen werden müssen, und eine Migration innerhalb der Netzwerkeinschränkungen ermöglicht.

Diese Vorgehensweise kann für die Übertragung von Daten aus dem HDFS, Sicherungen, Archiven sowie von Dateiservern und aus Anwendungen verwendet werden. In vorhandenen technischen Leitfäden wird erläutert, wie Daten auf diese Weise aus einem [HDFS-Speicher](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) oder mit [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) oder dem [Datenkopierdienst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) von Datenträgern in Data Box übertragen werden.

Es gibt auch Partnerlösungen von Drittanbietern, die Azure Data Box für die Migration verwenden. Mit diesen Lösungen übertragen Sie eine große Menge Daten offline, synchronisieren sie später aber in geringerem Umfang über das Netzwerk.

![Diagramm: Offline- und Onlinedatenübertragung mit Azure Data Box](../../_images/migrate/data-box.png)

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Wenn die Speicheranforderungen einer Workload (oder mehrerer Workloads) die Netzwerkkapazität übersteigen, kann Azure Data Box dennoch für eine Offlinedatenübertragung verwendet werden.

Die Netzwerkübertragung wird empfohlen, es sei denn, das Netzwerk ist nicht verfügbar. Die Übertragung von Daten über das Netzwerk ist selbst bei eingeschränkter Bandbreite normalerweise schneller als der physische Versand der Daten bei einer Offlineübertragungsmethode.

Wenn Konnektivität mit Azure verfügbar ist, sollten Sie vor der Verwendung von Data Box eine Analyse durchführen, vor allem, wenn bei der Migration der Workload die Dauer wichtig ist. Die Verwendung von Data Box ist nur dann sinnvoll, wenn die Übertragung der erforderlichen Daten länger dauert als das Übertragen auf den Datenträger, Versenden und Wiederherstellen.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Analyse der Netzwerkkapazität:** Wenn bei workloadbezogenen Anforderungen in Bezug auf die Datenübertragung eine Überschreitung der Netzwerkkapazität droht, fügt das Cloudeinführungsteam dem Bewertungsprozess als zusätzliche Analyseaufgabe die Analyse der Netzwerkkapazität hinzu. Bei dieser Analyse schätzt ein Mitglied des Teams die verfügbare Netzwerkkapazität und die für die Datenübertragung benötigte Zeit. Beachten Sie, dass dieses Teammitglied über Fachkenntnisse in Bezug auf das lokale Netzwerk und Netzwerkkonnektivität verfügen sollte.

Die verfügbare Kapazität wird anschließend mit den Speicheranforderungen aller im aktuellen Release zu migrierenden Ressourcen verglichen. Wenn die Speicheranforderungen die verfügbare Bandbreite übersteigen, werden die Ressourcen, die die Workload unterstützen, für die Offlineübertragung ausgewählt.

> [!IMPORTANT]
> Nach Abschluss der Analyse müssen Sie möglicherweise den Releaseplan aktualisieren, sodass die für den Versand, die Wiederherstellung und die Synchronisierung der offline zu übertragenden Ressourcen benötigte Zeit berücksichtigt wird.

**Abweichungsanalyse:** Überprüfen Sie alle offline zu übertragenden Ressourcen auf Speicher- und Konfigurationsabweichungen. Die *Speicherabweichung* ist der Umfang der Änderung des zugrunde liegenden Speichers im zeitlichen Verlauf. Die *Konfigurationsabweichung* ist die Änderung der Konfiguration der Ressource im zeitlichen Verlauf. Abweichungen zwischen dem Zeitpunkt, zu dem der Speicher kopiert wird, und dem Zeitpunkt, zu dem die Ressource höher gestuft wird in die Produktion, gehen möglicherweise verloren. Wenn diese Abweichung in der migrierten Ressource berücksichtigt werden soll, ist eine Synchronisierung zwischen der lokalen Ressource und der migrierten Ressource erforderlich. Diesen Hinweis sollten Sie zur Berücksichtigung bei der Durchführung der Migration kennzeichnen.

## <a name="migration-process-changes"></a>Änderungen für den Migrationsprozess

Wenn Sie Offlineübertragungsmethoden verwenden, sind in der Regel keine [Replikationsprozesse](../migration-considerations/migrate/replicate.md) erforderlich, [Synchronisierungsprozesse](../migration-considerations/migrate/replicate.md) hingegen möglicherweise schon. Wenn eine Ressource offline übertragen wird, geben die Ergebnisse der im Bewertungsprozess durchgeführten Abweichungsanalyse Auskunft über die bei der Migration erforderlichen Aufgaben.

### <a name="suggested-action-during-the-migration-process"></a>Empfohlene Aktion während des Migrationsprozesses

**Kopieren des Speichers:** Diese Vorgehensweise kann für die Übertragung von Daten aus dem HDFS, Sicherungen, Archiven sowie von Dateiservern und aus Anwendungen verwendet werden. In vorhandenen technischen Leitfäden wird erläutert, wie Daten auf diese Weise aus einem [HDFS-Speicher](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) oder mit [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) oder dem [Datenkopierdienst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) von Datenträgern in Data Box übertragen werden.

Es gibt auch Partnerlösungen von Drittanbietern, die Azure Data Box für die Migration verwenden. Mit diesen Lösungen übertragen Sie eine große Menge Daten offline, synchronisieren sie später aber in geringerem Umfang über das Netzwerk.

**Versenden des Geräts:** Wenn Sie die Daten kopiert haben, können Sie [das Gerät an Microsoft senden](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). Nach dem Empfang und Import sind die Daten in einem Azure Storage-Konto verfügbar.

**Wiederherstellen der Ressource:** [Überprüfen Sie, ob die Daten](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) im Speicherkonto verfügbar sind. Wenn dies der Fall ist, können Sie die Daten als Blob oder in Azure Files verwenden. Wenn es sich bei den Daten um eine VHD- oder VHDX-Datei handelt, können Sie diese in verwaltete Datenträger konvertieren. Die verwalteten Datenträger können dann zum Instanziieren eines virtuellen Computers verwendet werden, auf dem ein Replikat der ursprünglichen lokalen Ressource erstellt wird.

**Synchronisierung:** Wenn die Synchronisierung von Abweichungen für eine migrierte Ressource erforderlich ist, können Sie die Dateien mithilfe einer der Partnerlösungen von Drittanbietern synchronisieren, bis die Ressource wiederhergestellt ist.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Optimierungsaktivitäten sind von dieser Ergänzung wahrscheinlich nicht betroffen.

## <a name="secure-and-manage-process-changes"></a>Änderungen am Sicherungs- und Verwaltungsprozess

Sicherungs- und Verwaltungsaktivitäten sind von dieser Ergänzung wahrscheinlich nicht betroffen.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur Checkliste zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für bewährte Migrationsmethoden](./index.md)
