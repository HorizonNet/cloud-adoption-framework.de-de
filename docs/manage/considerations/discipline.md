---
title: Verwaltungsebenen bei der Cloudverwaltung
description: Es wird beschrieben, wie Sie die Cloudverwaltungsoptionen auf einen einheitlichen Satz mit Prozessen und Tools beschränken, den Sie für in der Cloud gehostete Workloads anbieten können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9571de511bbe037a35703f4ee64ef00edbe1745f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223999"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Verwaltungsebenen in den verschiedenen Cloudverwaltungsdisziplinen

Entscheidend für die ordnungsgemäße Verwaltung in einer Umgebung sind Konsistenz und wiederholbare Prozesse. Azure bietet Ihnen unendlich viele Optionen. Ebenso gibt es unzählige Ansätze für die Cloudverwaltung. Um Konsistenz und wiederholbare Prozesse zu gewährleisten, ist es wichtig, diese Optionen auf einen einheitlichen Satz von Verwaltungsabläufen und -tools einzugrenzen, die für in der Cloud gehostete Workloads angeboten werden.

## <a name="suggested-management-levels"></a>Empfohlene Verwaltungsebene

Da die Workloads in Ihrem IT-Portfolio variieren, ist es unwahrscheinlich, dass eine einzige Verwaltungsebene für alle ausreicht. Um Ihnen bei der Unterstützung einer Vielzahl von Workloads und geschäftlichen Verpflichtungen zu helfen, empfehlen wir, dass Ihr Cloudbetriebs- oder Plattformbetriebsteam einige Betriebsverwaltungsebenen einrichten.

![Verwalten von Verwaltungsebenen und Reifegrad im Framework für die Cloudeinführung](../../_images/manage/cloud-management-maturity.png)

Erwägen Sie als Ausgangspunkt die Festlegung der Verwaltungsebenen, die im vorhergehenden Diagramm dargestellt und in der folgenden Liste vorgeschlagen sind:

- **Verwaltungsbaseline**: Eine Baseline für die Cloudverwaltung (oder Verwaltungsbaseline) ist ein definierter Satz von Tools, Prozessen und konsistenten Preisen, der die Grundlage für die gesamte Cloudverwaltung in Azure bildet. Um eine Baseline für die Cloudverwaltung zu erstellen und zu ermitteln, welche Tools in das Baselineangebot für Ihr Unternehmen aufgenommen werden sollen, überprüfen Sie die Liste im Abschnitt „Cloudverwaltungsdisziplinen“.
- **Erweiterte Baseline**: Für einige Workloads können Erweiterungen der Baseline erforderlich sein, die nicht unbedingt spezifisch für eine einzelne Plattform oder Workload sind. Obwohl diese Erweiterungen nicht für jede Workload kostengünstig sind, sollte es für jede Workload einheitliche Prozesse, Tools und Lösungen geben, die die Kosten für die zusätzliche Unterstützung der Verwaltung rechtfertigen können.
- **Plattformspezialisierung:** In einer bestimmten Umgebung werden einige gängige Plattformen von einer Vielzahl von Workloads verwendet. Diese allgemeine Gemeinsamkeit hinsichtlich der Architektur bleibt auch dann bestehen, wenn Unternehmen die Cloud einführen. Die Plattformspezialisierung ist eine gehobene Verwaltungsebene, die das Fachwissen zu Daten und Architekturen anwendet, um die Betriebsverwaltung auf einer höheren Ebene zu gewährleisten. Beispiele für die Plattformspezialisierung sind spezifische Verwaltungsfunktionen für SQL Server, Container, Active Directory oder andere Dienste, die durch konsistente, wiederholbare Prozesse, Tools und Architekturen besser verwaltet werden können.
- **Workloadspezialisierung:** Für wirklich unternehmenskritischen Workloads kann es aus Kostengründen sinnvoll sein, viel tiefer in die Verwaltung dieser Workloads einzusteigen. Die Workloadspezialisierung wendet Workloadtelemetriedaten an, um weiterführende Ansätze für die tägliche Verwaltung zu bestimmen. Aus diesen Daten lassen sich oft Automatisierungs-, Bereitstellungs- und Entwurfsverbesserungen ableiten, die zu mehr Stabilität, Zuverlässigkeit und Ausfallsicherheit führen, als dies mit einer reinen Betriebsverwaltung möglich ist.
- **Nicht unterstützt**: Ebenso wichtig ist es, gemeinsame Verwaltungsprozesse zu kommunizieren, bei denen Workloads, die als nicht unterstützt oder nicht unternehmenskritisch eingestuft werden, nicht über Cloudverwaltungsdisziplinen bereitgestellt werden.

Unternehmen können auch [Funktionen, die mit einer oder mehreren dieser Verwaltungsebenen in Zusammenhang stehen, an einen Dienstanbieter auslagern](https://aka.ms/adopt/partneroffers). Diese Dienstanbieter können mit [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) mehr Genauigkeit und Transparenz bieten.

In den verbleibenden Artikeln dieser Reihe werden Prozesse beschrieben, die in jeder dieser Disziplinen gebräuchlich sind.
Gleichzeitig finden Sie im [Azure-Verwaltungsleitfaden](../azure-management-guide/index.md) eine Beschreibung der Tools, die diese Prozesse unterstützen können. Wenn Sie Unterstützung beim Aufbau Ihrer Verwaltungsbaseline benötigen, lesen Sie zunächst den Azure-Verwaltungsleitfaden. Nachdem Sie die Baseline festgelegt haben, können Sie sie mit den Informationen in dieser Artikelreihe und den dazugehörigen bewährten Methoden erweitern und weitere Ebenen der Verwaltungsunterstützung definieren.

## <a name="cloud-management-disciplines"></a>Cloudverwaltungsdisziplinen

Jede empfohlene Verwaltungsebene kann auf eine Vielzahl von Cloudverwaltungsdisziplinen zurückgreifen. Durch die Zuordnung ist es jedoch einfacher, die empfohlenen Prozesse und Tools für die jeweilige Cloudverwaltungsebene zu finden.

In den meisten Fällen besteht die zuvor erläuterte _Ebene der Verwaltungsbaseline_ aus Prozessen und Tools aus den folgenden Disziplinen. Es werden jeweils einige Prozesse und Tools hervorgehoben, um die _erweiterten Baselinefunktionen_ zu demonstrieren.

- **Bestand und Transparenz:** Die Verwaltungsbaseline erfordert mindestens eine Möglichkeit zur Bestandsaufnahme von Ressourcen und zur Schaffung von Transparenz über den Ausführungszustand jeder Ressource.
- **Betriebsbezogene Compliance:** Eine regelmäßige Verwaltung von Konfiguration, Größe, Kosten und Leistung von Ressourcen ist für die Erfüllung der Leistungserwartungen und für eine Verwaltungsbaseline unverzichtbar.
- **Schutz und Wiederherstellung:** Die Minimierung von Betriebsunterbrechungen und die Beschleunigung der Wiederherstellung können Ihnen dabei helfen, Leistungsverluste und Umsatzauswirkungen zu vermeiden. Erkennung und Wiederherstellung sind wesentliche Aspekte dieser Disziplin innerhalb einer Verwaltungsbaseline.

Die Verwaltungsebene der Plattformspezialisierung setzt sich aus den Prozessen und Tools zusammen, die mit den Disziplinen des Plattformbetriebs ausgerichtet sind. Ebenso setzt sich die Verwaltungsebene der Workloadspezialisierung aus den Prozessen und Tools zusammen, die mit den Disziplinen des Workloadbetriebs ausgerichtet sind.

## <a name="next-steps"></a>Nächste Schritte

Der nächste Schritt bei der Definition der einzelnen Ebenen der Cloudverwaltung sind Kenntnisse zu [Bestand und Transparenz](./inventory.md).

> [!div class="nextstepaction"]
> [Bestands- und Transparenzoptionen](./inventory.md)
