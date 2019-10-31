---
title: Verwaltungsebenen in den verschiedenen Cloudverwaltungsdisziplinen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verwaltungsebenen in den verschiedenen Cloudverwaltungsdisziplinen
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 44bfe58f86a442a5129eee791e3da0f7a6b68031
ms.sourcegitcommit: 73dbedf580951f25bf4b5544b83451cb075b1fa1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2019
ms.locfileid: "72805797"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Verwaltungsebenen in den verschiedenen Cloudverwaltungsdisziplinen

Entscheidend für die ordnungsgemäße Verwaltung in einer Umgebung sind Konsistenz und wiederholbare Prozesse. Azure bietet Ihnen unendlich viele Optionen. Ebenso gibt es unzählige Ansätze für die Cloudverwaltung. Um Konsistenz und wiederholbare Prozesse zu gewährleisten, ist es wichtig, diese Optionen auf einen einheitlichen Satz von Verwaltungsabläufen und -tools einzugrenzen, die für in der Cloud gehostete Workloads angeboten werden.

## <a name="suggested-management-levels"></a>Empfohlene Verwaltungsebene

Da die Workloads in Ihrem IT-Portfolio nicht alle gleich sind, ist es unwahrscheinlich, dass eine einzige Verwaltungsebene für alle ausreicht. Um verschiedene Workloads und geschäftliche Verpflichtungen zu unterstützen, wird empfohlen, dass das Cloudbetriebs- oder das Plattformbetriebsteam einige Betriebsverwaltungsebenen einrichten.

![Verwalten von Verwaltungsebenen und Reifegrad im Framework für die Cloudeinführung](../../_images/manage/cloud-management-maturity.png)

Im Folgenden finden Sie einige empfohlene Verwaltungsebenen (ebenfalls oben dargestellt), die als Ausgangspunkt dienen können:

- **Verwaltungsbaseline**: Eine Baseline für die Cloudverwaltung (oder Verwaltungsbaseline) ist ein definierter Satz von Tools, Prozessen und konsistenten Preisen, der die Grundlage für die gesamte Cloudverwaltung in Azure bildet. Um eine Baseline für die Cloudverwaltung zu erstellen, lesen Sie die Tabelle im folgenden Abschnitt, und legen Sie fest, welche Tools in das Baselineangebot für Ihr Unternehmen aufgenommen werden sollen.
- **Erweiterte Baseline**: Für einige Workloads können Erweiterungen der Baseline erforderlich sein, die nicht unbedingt spezifisch für eine einzelne Plattform oder Workload sind. Obwohl diese Erweiterungen nicht für jede Workload kostengünstig sind, sollte es für jede Workload einheitliche Prozesse, Tools und Lösungen geben, die eine zusätzliche Unterstützung der Verwaltung rechtfertigen können.
- **Plattformspezialisierung**: In jeder Umgebung gibt es gemeinsame Plattformen, die von mehreren verschiedenen Workloads genutzt werden. Diese allgemeine Gemeinsamkeit hinsichtlich der Architektur bleibt auch dann bestehen, wenn Unternehmen die Cloud einführen. Die Plattformspezialisierung ist eine gehobene Verwaltungsebene, die das Fachwissen zu Daten und Architekturen nutzt, um die Betriebsverwaltung auf einer höheren Ebene zu gewährleisten. Beispiele für die Plattformspezialisierung sind spezifische Verwaltungsfunktionen für SQL Server, Container, Active Directory oder andere Dienste, die durch konsistente, wiederholbare Prozesse, Tools und Architekturen besser verwaltet werden können.
- **Workloadspezialisierung**: Für die wirklich unternehmenskritischen Workloads kann es aus Kostengründen sinnvoll sein, viel tiefer in die Verwaltung dieser Workloads einzusteigen. Die Workloadspezialisierung nutzt Workloadtelemetriedaten, um weiterführende Ansätze für die tägliche Verwaltung zu bestimmen. Aus diesen Daten lassen sich oft Automatisierungs-, Bereitstellungs- und Entwurfsverbesserungen ableiten, die zu mehr Stabilität, Zuverlässigkeit und Ausfallsicherheit führen, als dies mit einer reinen Betriebsverwaltung möglich ist.
- **Nicht unterstützt**: Ebenso wichtig ist es, gemeinsame Verwaltungsprozesse zu kommunizieren, bei denen Workloads, die als nicht unterstützt oder nicht unternehmenskritisch eingestuft werden, nicht über Cloudverwaltungsdisziplinen bereitgestellt werden.

Unternehmen können auch [Funktionen, die mit einer oder mehreren dieser Verwaltungsebenen in Zusammenhang stehen, an einen Dienstanbieter auslagern](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Diese Dienstanbieter können mit [Azure Lighthouse](https://azure.com/lighthouse) mehr Genauigkeit und Transparenz bieten.

In den verbleibenden Artikeln dieser Reihe wird eine Reihe von Prozessen beschrieben, die in jeder dieser Disziplinen gebräuchlich sind.
Gleichzeitig finden Sie im [Azure-Verwaltungsleitfaden](../azure-management-guide/index.md) eine Beschreibung der Tools, die diese Prozesse unterstützen können. Wenn Sie Unterstützung beim Aufbau Ihrer Verwaltungsbaseline benötigen, lesen Sie zunächst den Azure-Verwaltungsleitfaden. Sobald die Baseline festgelegt ist, können Sie sie mit den Informationen in dieser Artikelreihe und den dazugehörigen Best Practices erweitern und weitere Ebenen der Verwaltungsunterstützung definieren.

## <a name="cloud-management-disciplines"></a>Cloudverwaltungsdisziplinen

Jede der empfohlenen Verwaltungsebenen kann auf unterschiedliche Cloudverwaltungsdisziplinen zurückgreifen. Durch die Zuordnung ist es jedoch einfacher, die empfohlenen Prozesse und Tools für die jeweilige Cloudverwaltungsebene zu finden.

In den meisten Fällen besteht die oben beschriebene Ebene der „Verwaltungsbaseline“ aus Prozessen und Tools aus den folgenden Disziplinen. Es werden jeweils einige Prozesse und Tools hervorgehoben, um die „erweiterten Baselinefunktionen“ zu demonstrieren.

- **Bestand und Transparenz**: Die Verwaltungsbaseline erfordert mindestens eine Möglichkeit zur Bestandsaufnahme von Ressourcen und zur Schaffung von Transparenz über den Ausführungszustand jeder Ressource.
- **Betriebsbezogene Compliance:** Eine regelmäßige Verwaltung von Konfiguration, Größe, Kosten und Leistung von Ressourcen ist für die Erfüllung der Leistungserwartungen und für eine Verwaltungsbaseline unverzichtbar.
- **Schutz und Wiederherstellung:** Die Minimierung von Betriebsunterbrechungen und die Beschleunigung der Wiederherstellung tragen dazu bei, Leistungsverluste und Umsatzauswirkungen zu vermeiden. Erkennung und Wiederherstellung sind wesentliche Aspekte dieser Disziplin innerhalb einer Verwaltungsbaseline.

Die Verwaltungsebene der Plattformspezialisierung setzt sich aus den Prozessen und Tools zusammen, die auf die Disziplinen des Plattformbetriebs ausgerichtet sind. Ebenso setzt sich die Verwaltungsebene der Workloadspezialisierung aus den Prozessen und Tools zusammen, die auf die Disziplinen des Workloadbetriebs ausgerichtet sind.

  
## <a name="next-steps"></a>Nächste Schritte

Der nächste Schritt bei der Definition der einzelnen Ebenen der Cloudverwaltung sind Kenntnisse zu [Bestand und Transparenz](./inventory.md).

> [!div class="nextstepaction"]
> [Bestands- und Transparenzoptionen](./inventory.md)
