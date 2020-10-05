---
title: Durchführen einer Überprüfung von Cloudrichtlinien
description: Hier erfahren Sie, wie Sie vorhandene IT-Richtlinien von Unternehmen modernisieren, um ein gleichwertiges Risikomanagement für cloudbasierte Ressourcen bereitzustellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8ab66a82b7677beb44fae256fade1ed1afd1173e
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108009"
---
# <a name="conduct-a-cloud-policy-review"></a>Durchführen einer Überprüfung von Cloudrichtlinien

Eine Überprüfung von Cloudrichtlinien ist der erste Schritt zur [Governance-Einsatzreife](../index.md) in der Cloud. Das Ziel dieses Prozesses ist eine Modernisierung der vorhandenen IT-Unternehmensrichtlinien. Nach seinem Abschluss bieten die aktualisierten Richtlinien eine gleichwertige Ebene des Risikomanagements für cloudbasierte Ressourcen. In diesem Artikel wird der Prozess zur Überprüfung von Cloudrichtlinien und deren Bedeutung erläutert.

## <a name="why-perform-a-cloud-policy-review"></a>Warum sollte eine Überprüfung von Cloudrichtlinien durchgeführt werden?

In den meisten Unternehmen wird die IT über die Ausführung von Prozessen verwaltet, die sich an den geltenden Richtlinien orientieren. In kleinen Unternehmen gibt es möglicherweise nur einzelne Richtlinien, und Prozesse sind ungenau definiert. Wenn aus Unternehmen Großunternehmen werden, werden Richtlinien und Prozesse tendenziell klarer dokumentiert und konsequenter ausgeführt.

Während Unternehmen für ausgereiftere IT-Unternehmensrichtlinien sorgen, gibt es bei Abhängigkeiten von den letzten technischen Entscheidungen die Tendenz, in leitende Richtlinien einzudringen. So kommt es beispielsweise häufig vor, dass Notfallwiederherstellungsprozesse Richtlinien enthalten, die Offsite-Bandsicherungen erfordern. Diese Bedingung setzt eine Abhängigkeit von einem einzigen Technologietyp (Bandsicherungen) voraus, der vielleicht nicht mehr die relevanteste Lösung ist.

Cloudtransformationen schaffen einen natürlichen Wendepunkt, um die Entscheidungen zu Legacyrichtlinien aus der Vergangenheit zu überdenken. Technische Funktionen und Standardprozesse ändern sich in der Cloud erheblich, genauso wie die Vererbungsrisiken. Im vorherigen Beispiel ist die Bandsicherungsrichtlinie auf das Risiko eines Single Point of Failure zurückzuführen, der sich durch die Speicherung der Daten an einem einzelnen Ort ergab und das Unternehmen dazu veranlasste, das Risikoprofil durch die Minderung dieses Risikos zu verbessern. In einer Cloudbereitstellung gibt es mehrere Optionen, die dieselbe Risikominderung mit viel geringeren RTOs (Recovery Time Objectives) bieten. Beispiel:

- Eine cloudnative Lösung könnte die Georeplikation von Azure SQL-Datenbank aktivieren.
- Eine Hybridlösung kann beispielsweise Azure Site Recovery nutzen, um eine IaaS-Workload in Azure zu replizieren.

Bei Ausführung einer Cloudtransformation steuern Richtlinien oft viele der Tools, Dienste und Prozesse, die für die Cloudeinführungsteams zur Verfügung stehen. Wenn diese Richtlinien auf älteren Technologien basieren, können sie die Bemühungen des Teams behindern, für Änderungen zu sorgen. Im schlimmsten Fall werden wichtige Richtlinien vom Migrationsteam vollständig ignoriert, um Problemumgehungen zu ermöglichen. Keines davon ist ein akzeptables Ergebnis.

## <a name="the-cloud-policy-review-process"></a>Der Prozess der Überprüfung von Cloudrichtlinien

Überprüfungen von Cloudrichtlinien gleichen vorhandene Richtlinien für IT-Governance und IT-Sicherheit an die [fünf Disziplinen von Cloudgovernance](../index.md) an:

- [Disziplin „Kostenverwaltung“](../cost-management/index.md)
- [Disziplin „Sicherheitsbaseline“](../security-baseline/index.md)
- [Disziplin „Identitätsbaseline“](../identity-baseline/index.md)
- [Disziplin „Ressourcenkonsistenz“](../resource-consistency/index.md)
- [Disziplin „Beschleunigung der Bereitstellung“](../deployment-acceleration/index.md)

Bei jeder dieser Disziplinen besteht der Überprüfungsprozess aus folgenden Schritten:

1. Überprüfung vorhandener lokaler Richtlinien im Hinblick auf die jeweilige Disziplin, wobei nach zwei wichtigen Datenpunkten gesucht wird: Legacyabhängigkeiten und identifizierte Geschäftsrisiken.
2. Bewerten Sie die einzelnen Geschäftsrisiken, indem Sie eine einfache Frage stellen: Ist das Geschäftsrisiko in einem Cloudmodell weiterhin vorhanden?
3. Falls ja, schreiben Sie die Richtlinie um, indem Sie die erforderliche Maßnahme (nicht die technische Lösung) dokumentieren.
4. Überprüfen Sie die aktualisierte Richtlinie zusammen mit den Cloudeinführungsteams, um mögliche technische Lösungen für die erforderliche Maßnahme zu verstehen.

## <a name="example-of-a-policy-review-for-a-legacy-policy"></a>Beispiel für eine Richtlinienüberprüfung bei einer Legacyrichtlinie

Als Beispiel für den erforderlichen Prozess wird die Bandsicherungsrichtlinie aus dem vorgehenden Abschnitt verwendet:

- Eine Unternehmensrichtlinie erfordert Offsite-Bandsicherungen für alle Produktionssysteme. In dieser Richtlinie gibt es zwei relevante Datenpunkte:
  - Legacyabhängigkeit bei einer Bandsicherungslösung.
  - Ein angenommenes Geschäftsrisiko im Zusammenhang mit der Speicherung von Sicherungen an demselben physischen Ort wie die Produktionsgeräte.
- Ist das Risiko weiterhin vorhanden? Ja. Sogar in der Cloud ist die Abhängigkeit von einem einzigen Standort mit einem gewissen Risiko verbunden. Zwar ist es weniger wahrscheinlich, dass sich dieses Risiko auf das Geschäft auswirkt, wie es bei der lokalen Lösung der Fall war, doch das Risiko besteht weiterhin.
- Schreiben Sie die Richtlinie um. Bei einem Notfall, der ein gesamtes Datencenter betrifft, muss es innerhalb von 24 Stunden nach dem Ausfall eine Möglichkeit zur Wiederherstellung von Produktionssystemen in einem anderen Datencenter und an einem anderen geografischen Standort geben.
  - Beachten Sie außerdem, dass der in der obigen Anforderung angegebene Zeitplan möglicherweise aufgrund von technischen Einschränkungen festgelegt wurde, die in der Cloud nicht mehr vorhanden sind. Machen Sie sich mit den technischen Einschränkungen und Funktionen der Cloud vertraut, bevor Sie einfach eine Legacy-RTO/RPO anwenden.
- Überprüfen Sie dies mit den Cloudeinführungsteams. Je nach implementierter Lösung gibt es mehrere Möglichkeiten zur Einhaltung dieser Richtlinie zur Ressourcenkonsistenz.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über das Einschließen der Datenklassifizierung in Ihre Cloud Governance-Strategie.

> [!div class="nextstepaction"]
> [Datenklassifizierung](./data-classification.md)
