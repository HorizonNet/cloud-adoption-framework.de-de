---
title: Vorbereiten einer migrierten Anwendung für das Höherstufen zur Produktion
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit der Überprüfung vertraut zu machen, die beim Vorbereiten einer migrierten Anwendung für die Höherstufung in die Produktion durchgeführt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2ad912c7bc2e61465a81e278714f5018c2373f7f
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80429233"
---
# <a name="prepare-a-migrated-application-for-production-promotion"></a>Vorbereiten einer migrierten Anwendung für das Höherstufen zur Produktion

Nach dem Höherstufen einer Workload wird Datenverkehr von Produktionsbenutzern auf die migrierten Ressourcen weitergeleitet. Bereitschaftsaktivitäten bieten die Möglichkeit, die Workload auf diesen Datenverkehr vorzubereiten. Es folgen einige Überlegungen zu geschäftlichen und technologischen Aspekten, die Sie durch die Bereitschaftsaktivitäten führen.

## <a name="validate-the-business-change-plan"></a>Überprüfen des geschäftsbezogenen Änderungsplans

Transformation geschieht, wenn geschäftliche Benutzer und Kunden von einer technischen Lösung profitieren, die Prozesse ausführt, die das Unternehmen steuern. Bereitschaft ist eine gute Gelegenheit, den [geschäftsbezogenen Änderungsplan](./business-change-plan.md) zu überprüfen und sicherzustellen, dass damit angemessenes Training für geschäftliche und technische Teams verbunden ist. Stellen Sie insbesondere sicher, dass die folgenden technologiebezogenen Aspekte des Plans ordnungsgemäß kommuniziert werden:

- Training der Endbenutzer ist abgeschlossen (oder zumindest geplant).
- Ausfallzeitenfenster wurden ggf. kommuniziert und genehmigt.
- Produktionsdaten wurden synchronisiert und von Endbenutzern überprüft.
- Überprüfen Sie das Timing für Einführung und Höherstufen; Stellen Sie sicher, dass Zeitpläne und Änderungen an Endbenutzer kommuniziert wurden.

## <a name="final-technical-readiness-tests"></a>Letzte Tests der technischen Bereitschaft

*Bereit* ist der letzte Schritt vor der Freigabe für die Produktionsumgebung. Das bedeutet, dass dies auch die letzte Chance ist, die Workload zu testen. Im Folgenden finden Sie einige Tests, die für diese Phase vorgeschlagen werden:

- **Netzwerkisolationstest.** Testen und überwachen Sie den Netzwerkdatenverkehr, um zu gewährleisten, dass die Isolation fehlerfrei ist und keine unerwarteten Netzwerksicherheitsrisiken auftreten. Stellen Sie auch sicher, dass bei einem während der Umstellung unterbrochenen Netzwerkrouting kein unvorhergesehener Datenverkehr auftritt.
- **Abhängigkeitstest.** Stellen Sie sicher, dass alle Workloadanwendungsabhängigkeiten migriert wurden und von den migrierten Ressourcen darauf zugegriffen werden kann.
- **Test von Geschäftskontinuität und Notfallwiederherstellung (BCDR, Business Continuity und Disaster Recovery).** Überprüfen Sie, ob alle SLAs für Sicherung und Wiederherstellung eingerichtet sind. Führen Sie nach Möglichkeit eine vollständige Wiederherstellung der Ressourcen von der BCDR-Lösung durch.
- **Test des Endbenutzerroutings.** Überprüfen Sie Datenverkehrsmuster und Routing für den Endbenutzer-Datenverkehr. Stellen Sie sicher, dass die Leistung des Netzwerks den Erwartungen entspricht.
- **Letzte Leistungsüberprüfung.** Stellen Sie sicher, dass die Leistungstests abgeschlossen und von den Endbenutzern genehmigt wurden. Führen Sie beliebige automatisierte Leistungstests durch.

## <a name="final-business-validation"></a>Letzte Geschäftsvalidierung

Nach Validierung von geschäftsbezogenem Änderungsplan und technischer Bereitschaft können Sie mit den folgenden Schritten die Geschäftsvalidierung abschließen:

- **Kostenvalidierung (Kosten nach Plan im Vergleich zu tatsächlichen Kosten).** Das Testen führt wahrscheinlich zu Änderungen von Größe und Architektur. Stelle Sie sicher, dass die tatsächlichen Bereitstellungskosten immer noch mit dem ursprünglichen Plan übereinstimmen.
- **Kommunizieren und Ausführen des Umstellungsplans.** Kommunizieren Sie die Umstellung im Vorhinein, und führen Sie sie entsprechend aus.

## <a name="next-steps"></a>Nächste Schritte

Nach dem Abschluss aller Bereitschaftsaktivitäten ist es Zeit, die [Workload höher zu stufen](./promote.md).

> [!div class="nextstepaction"]
> [Was ist erforderlich, um eine migrierte Ressource in die Produktion höher zu stufen?](./promote.md)
