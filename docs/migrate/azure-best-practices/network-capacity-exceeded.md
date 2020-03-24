---
title: Netzwerkkapazität überschritten
description: Datenanforderungen überschreiten Netzwerkkapazität während einer Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 565cb0d97fc764375f708d8e3db8f2a1c0a852e4
ms.sourcegitcommit: d660484d534bc61fc60470373f3fcc885a358219
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508371"
---
<!-- cSpell:ignore HDFS databox VHDX -->

# <a name="data-requirements-exceed-network-capacity-during-a-migration-effort"></a>Datenanforderungen überschreiten Netzwerkkapazität während einer Migration

Bei einer Cloudmigration werden Ressourcen über das Netzwerk zwischen dem vorhandenen Rechenzentrum und der Cloud repliziert und synchronisiert. Es ist nicht ungewöhnlich, dass die vorhandenen Datengrößenanforderungen von verschiedenen Workloads die Netzwerkkapazität überschreiten. In einem solchen Szenario kann der Migrationsprozess sich drastisch verlangsamen oder in einigen Fällen ganz beendet werden. Die folgende Anleitung erweitert den Umfang des [Leitfadens zur Azure-Migration](../azure-migration-guide/index.md) und bietet eine Lösung zum Umgehen von Netzwerkbeschränkungen.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die meisten Aufgaben dieser Umfangserweiterung finden in den Prozessen für die Erfüllung von Voraussetzungen, die Bewertung und die Optimierung einer Migration statt.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

**Überprüfen von Risiken der Netzwerkkapazität:** Die [Rationalisierung digitaler Ressourcen](../../digital-estate/rationalize.md) ist eine dringend empfohlene Voraussetzung, insbesondere was die Problematik der Überlastung der verfügbaren Netzwerkkapazität angeht. Bei der Rationalisierung digitaler Ressourcen wird ein [Bestand digitaler Ressourcen](../../digital-estate/inventory.md) erfasst. Dieser Bestand sollte die vorhandenen Speicheranforderungen für die digitalen Ressourcen enthalten. Wie unter [Replikationsrisiken – Physikalische Grundlagen der Replikation](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) beschrieben, kann anhand des Bestands die **Gesamtgröße der Migrationsdaten** geschätzt und mit der gesamten **verfügbaren Migrationsbandbreite** verglichen werden. Wenn dieser Vergleich nicht mit der erforderlichen **Zeit bis zur Geschäftsänderung** übereinstimmt, kann dieser Artikel Ihnen helfen, die Migrationsgeschwindigkeit zu beschleunigen und die für die Migration des Rechenzentrums erforderliche Zeit zu verringern.

**Offlineübertragung von unabhängigen Datenspeichern:** In der nachfolgenden Abbildung sind Beispiele für die Onlinedatenübertragung sowie die Offlinedatenübertragung mit Azure Data Box dargestellt. Diese Ansätze können verwendet werden, um große Datenmengen vor der Workloadmigration in die Cloud zu versenden. Bei einer Offlinedatenübertragung werden die Quelldaten auf den Azure Data Box-Datenträger kopiert, der dann zur Übertragung als Datei oder Blob in ein Azure Storage-Konto physisch an Microsoft versendet wird. Bei diesem Vorgang können Daten versendet werden, die nicht direkt an eine bestimmte Workload gebunden sind, bevor andere Migrationsvorgänge durchgeführt werden. Dadurch wird die Menge der Daten reduziert, die über das Netzwerk übertragen werden müssen, um eine Migration innerhalb der Netzwerkeinschränkungen abschließen zu können.

Diese Vorgehensweise kann für die Übertragung von Daten aus HDFS, Sicherungen, Archiven, Dateiservern und Anwendungen verwendet werden. In vorhandenen technischen Anleitungen wird erläutert, wie Daten auf diese Weise aus [einem HDFS-Speicher](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) oder mithilfe von [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) oder des [Datenkopierdiensts](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) von Datenträgern in Data Box übertragen werden.

Es gibt auch [Partnerlösungen von Drittanbietern](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), bei denen Azure Data Box für eine „Seed & Feed“-Migration verwendet wird, wobei eine große Datenmenge über eine Offlineübertragung verschoben wird, später aber in geringerem Umfang über das Netzwerk synchronisiert wird.

![Offline- und Onlinedatenübertragung mit Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Wenn die Speicheranforderungen einer Workload (oder mehrerer Workloads) die Netzwerkkapazität überschreiten, kann Azure Data Box dennoch weiterhin für eine Offlinedatenübertragung verwendet werden.

Die Netzwerkübertragung wird empfohlen, es sei denn, das Netzwerk ist nicht verfügbar. Die Geschwindigkeit der Datenübertragung über das Netzwerk (selbst bei eingeschränkter Bandbreite) ist normalerweise schneller als der physische Versand derselben Datenmenge mithilfe einer Offlineübertragungsmethode wie z. B. Data Box.

Wenn die Verbindung mit Azure verfügbar ist, sollte vor Verwendung von Data Box eine Analyse durchgeführt werden, vor allem dann, wenn bei der Migration der Workload die Zeit wichtig ist. Data Box ist nur dann sinnvoll, wenn die Übertragung der erforderlichen Daten länger dauert als das Füllen, Versenden und Wiederherstellen der Daten mithilfe von Data Box.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Analyse der Netzwerkkapazität:** Wenn workloadbezogene Anforderungen in Bezug auf die Datenübertragung Gefahr laufen, die Netzwerkkapazität zu überschreiten, würde das Cloudeinführungsteam dem Bewertungsprozess als zusätzliche Analyseaufgabe die Analyse der Netzwerkkapazität hinzufügen. Während dieser Analyse schätzt ein Teammitglied mit Fachkenntnissen bezüglich des lokalen Netzwerks und der Netzwerkverbindung die verfügbare Netzwerkkapazität und die erforderliche Zeit für die Datenübertragung. Diese verfügbare Netzwerkkapazität wird mit den Speicheranforderungen aller im aktuellen Release zu migrierenden Ressourcen verglichen. Wenn die Speicheranforderungen die verfügbare Bandbreite überschreiten, werden Ressourcen, die die Workload unterstützen, für die Offlineübertragung ausgewählt.

> [!IMPORTANT]
> Nach Abschluss der Analyse muss der Releaseplan unter Umständen aktualisiert werden, um die Zeit anzugeben, die für den Versand, die Wiederherstellung und die Synchronisierung der offline zu übertragenden Ressourcen benötigt wird.

**Abweichungsanalyse:** Jede offline zu übertragende Ressource sollte auf Speicher- und Konfigurationsabweichungen analysiert werden. Die Speicherabweichung ist das Ausmaß der Änderungen im zugrunde liegenden Speicher im zeitlichen Verlauf. Die Konfigurationsabweichung ist die Änderung in der Konfiguration der Ressource im zeitlichen Verlauf. Ab dem Zeitpunkt, an dem der Speicher kopiert wird, bis zu dem Zeitpunkt, an dem die Ressource in die Produktion hochgestuft wird, kann eine Abweichung verloren gehen. Wenn diese Abweichung in der migrierten Ressource berücksichtigt werden soll, ist eine Synchronisierung zwischen der lokalen Ressource und der migrierten Ressource erforderlich. Dies sollte zur Berücksichtigung bei der Durchführung der Migration gekennzeichnet werden.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Bei Verwendung von Methoden zur Offlineübertragung sind [Replikationsprozesse](../migration-considerations/migrate/replicate.md) wahrscheinlich nicht erforderlich. [Synchronisierungsprozesse](../migration-considerations/migrate/replicate.md) können dagegen weiterhin erforderlich sein. Die Ergebnisse der im Bewertungsprozess durchgeführten Abweichungsanalyse geben Auskunft über die während der Migration erforderlichen Aufgaben, wenn eine Ressource offline übertragen wird.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

**Kopieren des Speichers:** Diese Vorgehensweise kann für die Übertragung von HDFS-Daten, Sicherungen, Archiven, Dateiservern oder Anwendungen verwendet werden. In vorhandenen technischen Anleitungen wird erläutert, wie Daten auf diese Weise aus [einem HDFS-Speicher](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) oder mithilfe von [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) oder des [Datenkopierdiensts](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) von Datenträgern in Data Box übertragen werden.

Es gibt auch [Partnerlösungen von Drittanbietern](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box), bei denen Azure Data Box für eine „Seed & Sync“-Migration verwendet wird, wobei eine große Datenmenge über eine Offlineübertragung verschoben wird, später aber in geringerem Umfang über das Netzwerk synchronisiert wird.

**Versenden des Geräts:** Nach dem Kopieren der Daten kann das Gerät [an Microsoft versendet werden](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). Nach dem Empfang und dem Import sind die Daten in einem Azure Storage-Konto verfügbar.

**Wiederherstellen der Ressource:** [Überprüfen Sie, ob die Daten](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) im Speicherkonto verfügbar sind. Nach der Überprüfung können die Daten als Blob oder in Azure Files verwendet werden. Wenn es sich bei den Daten um eine VHD/VHDX-Datei handelt, kann diese Datei in verwaltete Datenträger konvertiert werden. Die verwalteten Datenträger können dann zum Instanziieren eines virtuellen Computers verwendet werden, auf dem ein Replikat der ursprünglichen lokalen Ressource erstellt wird.

**Synchronisierung:** Wenn die Synchronisierung von Abweichungen für eine migrierte Ressource erforderlich ist, können die Dateien mithilfe einer der [Partnerlösungen von Drittanbietern](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) synchronisiert werden, bis die Ressource wiederhergestellt wird.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Optimierungsaktivitäten sind von dieser Änderung des Umfangs wahrscheinlich nicht betroffen.

## <a name="secure-and-manage-process-changes"></a>Änderungen am Sicherungs- und Verwaltungsprozess

Sicherungs- und Verwaltungsaktivitäten sind von dieser Änderung des Umfangs sehr wahrscheinlich nicht betroffen.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
