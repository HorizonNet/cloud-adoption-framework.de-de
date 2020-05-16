---
title: Was ist eine Zielzone?
description: Hier finden Sie Informationen zu Landezonen – den Grundbausteinen jeder Cloudeinführungsumgebung.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: adef9ff5b7b32d91f3a7e32dd489804a90e7e7d7
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222945"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Was ist eine Zielzone?

Infrastructure-as-Code ist bei den meisten Cloudeinführungsaufgaben eine allgemeine Anforderung. Durch die Umstellung auf eine Code-First-Umgebung kann sich eine Lernkurve für Teammitglieder ergeben, und es müssen ggf. Änderungen an Aspekten des Betriebs sowie der Sicherheit, Governance und Konformität vorgenommen werden. Die Bereitstellung zweckbezogener Zielzonen hilft Ihnen, diese Kurven flacher zu halten, damit das Team die Einführungspläne sicher einhalten kann. In diesem Artikel werden der Begriff _Zielzone_ und andere verwandte Begriffe definiert. In anderen Artikeln dieser Serie wird die Erstellung von Zielzonen erläutert.

## <a name="pre-requisite-to-landing-zone-deployment"></a>Voraussetzung für die Bereitstellung von Zielzonen

Vor dem Definieren von Zielzonen ist es wichtig, einen verwandten Begriff zu verstehen: _Plattformumgebung_. In jeder Umgebung (Cloud, lokal oder hybrid) finden Sie eine Sammlung von _Umgebungshilfsprogrammen_, die die verschiedenen Workloads unterstützen. Das Unternehmen benötigt die Workloads für den Betrieb. Die IT-Abteilung benötigt diese grundlegenden Hilfsprogramme, um das vollständige _Portfolio_ der Workloads zu verwalten, zu steuern und zu sichern. Weitere Informationen zu diesen verwandten Begriffen und ihrem Zusammenhang finden Sie im Artikel zur [Portfoliohierarchie](../../reference/fundamental-concepts/hosting-hierarchy.md).

**Plattformumgebung:** Vor dem Bereitstellen von Zielzonen wird davon ausgegangen, dass zentralisierte Steuerungen für Identität, Sicherheit, Betrieb, Compliance und Governance für die Zielzone aus einer freigegebenen _Platformumgebung_ bereitgestellt werden, die alle Workloads in dieser speziellen Cloudplattform unterstützt. Alle Workloads in jeder Zielzone werden von diesen zentralen Kontrollen gesteuert, um eine konsistente Baseline für die _gemeinsamen Architektursäulen_ Sicherheit, Zuverlässigkeit, Leistung, Kosten und Cloudvorgänge einzurichten. 

**Aufgabentrennung:** Es sollte eine klare Trennung der Aufgaben zwischen den workloadbezogenen Aufgaben innerhalb einer Zielzone und der Nutzung der Hilfsprogramme bestehen, die außerhalb der Zielzone verwaltet werden. Diese Aufgabentrennung gewährleistet ordnungsgemäße Governance und Konformität. Außerdem wird sichergestellt, dass jedes Team alle Ausnahmen für die Unternehmensrichtlinie erläutert und berücksichtigt, um das schnelle Erstellen von Problemumgehungen zu vermeiden, die Ihre Umgebung gefährden könnten.

> [!CAUTION]
> Die Aufgabentrennung sollte nicht verhindern, dass Teams diese bewährte Methode ausschließlich auf Grundlage der aktuellen Personalzuweisung oder Teamstrukturen verwenden. Während der frühen Phase der Einführung der Cloud kann ein einzelnes Einführungsteam die Verantwortung für die Einführung von Cloudtechnologie und die Bereitstellung von Governance, Sicherheit und Betrieb für eine kleine Anzahl von Workloads vorübergehend übernehmen. Wenn der Plan für die Zukunft Aufgabentrennung oder sogar die Isolation von Aufgaben vorsieht, ist dieser Ansatz noch immer die empfohlene bewährte Methode.

**Gemeinsame Zuständigkeiten:** Die _Plattformumgebung_ stellt zentralisierte Kontrollen bereit, um die Cloudplattform zu steuern. Allerdings gibt es immer noch eine gemeinsame Verantwortung für alle Mitglieder des Teams, um die Anforderungen an Identität, Sicherheit, Betrieb, Compliance und Governance zu berücksichtigen. Bevor Sie eine Technologie in einer Zielzone einsetzen, sollten Sie verstehen, welche Hilfsprogramme von der _Plattformumgebung_ bereitgestellt werden und was Sie in der Zielzone implementieren müssen, um ihre gemeinsamen Zuständigkeiten zu erfüllen.

> [!IMPORTANT]
> Entwickler und Architekten, die Lösungen innerhalb einer Zielzone bereitstellen, können auf [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/) verweisen, um diese gemeinsamen Architektursäulen zu integrieren und zu erstellen, wenn sie Workloads entwerfen, erstellen oder unterstützen, die in einer Zielzone ausgeführt werden.

## <a name="landing-zone-definition"></a>Definition der Zielzone

Eine _Zielzone_ ist ein Segment einer Cloudumgebung, das vorab durch Code bereitgestellt wurde und für die Unterstützung **mindestens einer Workload** reserviert ist. Zielzonen ermöglichen den Zugriff auf grundlegende Tools und Steuerungen, um einen kompatiblen Ort zu schaffen, um Innovationen zu schaffen und neue Workloads in der Cloud zu erstellen oder vorhandene Workloads in die Cloud zu migrieren. In Zielzonen werden definierte Clouddienste und bewährte Methoden verwendet, um Ihren Erfolg zu gewährleisten.

Genauer gesagt, ist eine Zielzone der Grundbaustein jeder Cloudeinführungsumgebung. Der Begriff _Zielzone_ bezieht sich auf ein logisches Konstrukt, das es ermöglicht, dass Workloads in einer _Plattformumgebung_ koexistieren können. Zielzonen und die Plattformumgebung definieren gemeinsam alles, was vorhanden und bereit sein muss, um die Cloudeinführung im gesamten IT-Portfolio zu ermöglichen.

**Bereich:** Eine voll funktionsfähige Zielzone berücksichtigt alle Plattformhilfsprogramme, die zur Unterstützung der Anforderungen an eine Cloudeinführung des Kunden erforderlich sind.

**Refactoring:** Bei jeder Iteration der Bereitschaftsmethodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework) wird letztendlich eine voll funktionsfähige Landezone angestrebt. Während jeder Iterationen wird die Codebasis, die die Zielzone definiert, umgestaltet oder erweitert. Nach dem Refactoring kann die Zielzone geändert oder erneut bereitgestellt werden, um neue Anforderungen an die Cloud zu ermöglichen.

**Ziel:** Das Ziel des Ansatzes der Zielzone besteht darin, einen gemeinsamen Satz konsistenter Plattformimplementierungen zu erstellen, mit denen die Einführungsteams auf einer zentral verwalteten _Plattformgrundlage_ aufbauen können. Diese konsistenten Implementierungen müssen vorhanden sein, um sicherzustellen, dass Ihre Anwendungen bei der Bereitstellung Zugriff auf erforderliche Komponenten haben. Jede Zielzoneniterationen muss entsprechend den Anforderungen des Migrationsplans für die Cloud und der Abonnemententwurfsstrategie entworfen und bereitgestellt werden.

**Grundlegender Zweck:** Der Hauptzweck der Zielzone besteht darin, sicherzustellen, dass die erforderlichen Grundlagen und andere Hilfsprogramme bereits vorhanden sind, wenn eine Anwendung in die Cloud verschoben wird.

**Vorteile:** Zielzonen und eine allgemeine Plattformumgebung gewährleisten gemeinsam Konsistenz für die _gemeinsamen architektonischen Säulen_ Sicherheit, Zuverlässigkeit, Leistung, Kosten und Cloudvorgänge. Diese Kombination reduziert auch den Mehraufwand, der erforderlich ist, um Vorgänge, Governance und Konformität im gesamten IT-Portfolio aufrechtzuerhalten. Wenn die Einführungsanforderungen zunehmen, minimieren Zielzonen die Umgestaltung und Bereitstellung, die für die Skalierung ihrer Einführungsanforderungen erforderlich ist.

## <a name="landing-zone-usage"></a>Nutzung der Zielzone

Bei Zielzonen wird nicht unbedingt zwischen der Einführung von IaaS oder PaaS unterschieden. Allerdings sind Zielzonen speziell für die Unterstützung des Einführungsplans konzipiert, indem die Abonnementstrategie erfüllt wird. Die Unterstützung des Einführungsplans erfordert möglicherweise mehrere Zielzonen mit einer Mischung aus erforderlichen Komponenten.

Zweck und Umfang des Gesamtplans zur Einführung der Cloud bestimmen, welche Grundlagen erforderlich sind. Zusätzliche Anforderungen an Governance, Compliance, Sicherheit und Betriebsverwaltung werden wahrscheinlich den ursprünglichen Umfang der Zielzone erweitern. In frühen Phasen der Einführung können Zielzonen aufgrund von definierten Anforderungen und akzeptablen Risiken weniger Grundlagen umfassen. Wenn mehrere Zielzonen vorhanden sind, ist es sehr üblich, dass jede Zielzone von Hubs abhängig ist, die die erforderlichen Steuerelemente über ein freigegebenes Dienstmodell bereitstellen.

## <a name="decentralized-operations"></a>Dezentralisierte Vorgänge

In einigen dezentralisierten Organisationen werden durch Einführungsentwürfe Workloadteams erforderlich, die **Alleinverantwortung** für Ihre eigene Implementierung und den Betrieb der einzelnen isolierten Workloads tragen, einschließlich Sicherheit, Governance, Betriebsverwaltung und anderen Funktionen. Für diese Teams kann eine Workload möglicherweise über eine eigene getrennte Umgebung ohne Abhängigkeiten von einer Plattformumgebung verfügen. Diese workloadspezifischen Umgebungen weisen inkonsistente Implementierungen von Sicherheit, Zuverlässigkeit, Leistung, Kosten und Cloudvorgängen auf. Daher sollten Sie nicht als Zielzonen bezeichnet werden. Diese Teams sollten Anleitungen des [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/) nutzen, um die Workload unabhängig zu entwerfen, zu erstellen und zu optimieren.

> [!IMPORTANT]
> Ähnlich, aber etwas anders: In der frühen Phase des Cloudeinführungs-Lebenszyklus können kleinere Teams aufgrund von Notwendigkeiten wie dezentralisierte Organisationen arbeiten. Wenn diese Teams durch bestimmte Umstände dezentralisiert sind (im Gegensatz zu einer gewollten Dezentralisierung), sollte die bewährte Methode der Zielzone dennoch angewendet werden.

## <a name="portfolio-hierarchy"></a>Portfoliohierarchie

Zielzonen sind eine Ebene der gesamten Portfoliohierarchie, wie in den Voraussetzungen beschrieben. Das Vorhandensein von Zielzonen ist ein Indikator dafür, dass das Unternehmen ein umfassenderes Portfolio unterstützt. Dabei werden verschiedene unterstützende Teams, Prozesse und eine zentralisierte _Plattformumgebung_ eingesetzt. Weitere Informationen dazu, wie Zielzonen in den größeren Portfolioentwurf passen, finden Sie im Artikel zur [Portfoliohierarchie](../../reference/fundamental-concepts/hosting-hierarchy.md). Weitere Informationen zu den Produkten in Azure, die zum Verwalten der verschiedenen Ebenen der Portfoliohierarchie verwendet werden können, finden Sie im Artikel zur [Azure-Hierarchieunterstützung](../../reference/fundamental-concepts/hierarchy-azure-tools.md).

## <a name="next-steps"></a>Nächste Schritte

Bevor Ihre erste Zielzone einrichten, sollten Sie sich mit den [Refactoringprinzipien](./refactor.md) vertraut machen, auf denen dieser Ansatz beruht.

> [!div class="nextstepaction"]
> [Umgestalten von Zielzonen](./refactor.md)
