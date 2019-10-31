---
title: Benchmarking und Größenänderung von Cloudressourcen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Benchmarking und Größenänderung von Cloudressourcen
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 53ff6f0d32b80ef9c89d4ebd0234dd3442412907
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548425"
---
# <a name="benchmark-and-resize-cloud-assets"></a>Benchmarking und Größenänderung von Cloudressourcen

Das Überwachen von Nutzung und Ausgaben ist für Cloudinfrastrukturen von entscheidender Bedeutung. Organisationen zahlen für die Ressourcen, die sie im Laufe der Zeit nutzen. Wenn die Nutzung die Schwellenwerte der Vereinbarung übersteigt, können sich schnell unerwartete Kostenüberschreitungen ansammeln. Mit Cost Management-Berichten werden Ausgaben überwacht, um die Cloudnutzung, Kosten und Trends zu analysieren und nachzuverfolgen. Mithilfe von Berichten für den Zeitverlauf werden Anomalien erkannt, die von den normalen Trends abweichen. Ineffizienzen bei der Cloudbereitstellung werden in Optimierungsberichten angezeigt. Beachten Sie Ineffizienzen in Kostenanalyseberichten.

Bei den herkömmlichen lokalen IT-Modellen ist die Anforderung von IT-Systemen kosten- und zeitaufwendig. Die Prozesse erfordern oft langwierige Investitionsprüfungszyklen und können sogar einen jährlichen Planungsprozess erfordern. Daher ist es üblich, mehr als nötig zu kaufen. Es ist ebenso üblich, dass IT-Administratoren als Vorbereitung auf erwartete zukünftige Anforderungen Ressourcen im Übermaß bereitstellen.

In der Cloud entfallen durch die Kostenrechnungs- und Bereitstellungsmodelle die Zeitverzögerungen, die zu Überkäufen führen. Wenn zusätzliche Ressourcen benötigt werden, kann beinahe sofort zentral oder horizontal hochskaliert werden. Das bedeutet, dass Assets sicher verkleinert werden können, um Ressourcen- und Kostenaufwand zu minimieren. Beim Benchmarking und bei der Optimierung versucht das Cloudeinführungsteam, ein ausgewogenes Verhältnis zwischen Leistung und Kosten zu finden, indem Ressourcen bereitgestellt werden, die nicht größer oder kleiner sind, als es der Produktionsbedarf erfordert.

<!-- markdownlint-disable MD026 -->

## <a name="should-assets-be-optimized-during-or-after-the-migration"></a>Sollten Ressourcen während oder nach der Migration optimiert werden?

Wann sollte eine Ressource optimiert werden &mdash; während oder nach der Migration? Die einfache Antwort lautet: *in beiden Fällen*. Das ist aber nicht ganz zutreffend. Zur Erläuterung sind nachfolgend zwei grundlegende Szenarien für die Optimierung der Ressourcengröße angegeben:

- **Geplante Größenänderung.** Häufig ist eine Ressource deutlich zu groß und nicht ausgelastet, und ihre Größe sollte während der Bereitstellung geändert werden. Um festzustellen, ob die Größe einer Ressource erfolgreich geändert wurde, ist in diesem Fall ein Benutzerakzeptanztest nach der Migration erforderlich. Wenn ein Poweruser keine Leistungs- oder Funktionalitätsverluste während des Tests feststellt, kann davon ausgegangen werden, dass die Größe der Ressource erfolgreich geändert wurde.
- **Optimierung.** In Fällen, in denen der Optimierungsbedarf unklar ist, sollten IT-Teams einen datengesteuerten Ansatz zur Verwaltung der Ressourcengröße verwenden. Anhand von Benchmarks der Ressourcenleistung kann ein IT-Team fundierte Entscheidungen zu den Aspekten Größe, Dienste, Skalierung und Architektur einer Lösung treffen, die sich am besten für diese Lösung eignen. Es können dann nach der Migration Größenänderungen vorgenommen und Leistungstheorien getestet werden.

Verwenden Sie während der Migration fundierte Vermutungen, und experimentieren Sie mit der Größe. Für eine echte Ressourcenoptimierung sind jedoch Daten erforderlich, die auf der tatsächlichen Leistung in einer Cloudumgebung basieren. Damit eine echte Optimierung stattfinden kann, muss das IT-Team zunächst Methoden zur Überwachung von Leistung und Ressourcennutzung implementieren.

## <a name="benchmark-and-optimize-with-azure-cost-management"></a>Benchmarking und Optimierung mit Azure Cost Management

[Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview) ist durch Cloudyn, einem Tochterunternehmen von Microsoft, lizenziert und verwaltet Cloudausgaben transparent und präzise. Dieser Dienst sorgt für Überwachung, Benchmarking, Zuteilung und Optimierung von Cloudkosten.

Verlaufsdaten können beim Verwalten von Kosten helfen, indem Nutzung und Kosten im zeitlichen Verlauf analysiert werden, um Trends zu erkennen, die dann zur Prognose zukünftiger Ausgaben verwendet werden. Die Kostenverwaltung enthält ebenfalls nützliche projizierte Kostenberichte. Die Kostenzuteilung verwaltet Kosten, indem diese basierend auf Tagrichtlinien analysiert werden. Verwenden Sie die Kostenzuteilung für Showback und die verbrauchsbasierte Kostenzuteilung, um die Ressourcennutzung und die zugehörigen Kosten anzuzeigen und das Nutzungsverhalten zu beeinflussen oder diese Mandantenkunden in Rechnung zu stellen. Die Zugriffssteuerung unterstützt Sie beim Verwalten der Kosten, indem sichergestellt wird, dass Benutzer und Teams nur auf die Cost Management-Daten zugreifen können, die sie benötigen. Warnungen unterstützen Sie beim Verwalten der Kosten durch eine automatische Benachrichtigung, wenn ungewöhnliche Ausgaben oder eine Budgetüberschreitung auftreten. Durch Warnungen können auch andere Beteiligte automatisch über Anomalien bei den Ausgaben und das Risiko einer Budgetüberschreitung benachrichtigt werden. Verschiedene Berichte unterstützen Warnungen, die auf dem Budget und auf Kostenschwellenwerten basieren.

## <a name="improve-efficiency"></a>Verbessern der Effizienz

Mit Cost Management können Sie die optimale Nutzung virtueller Computer bestimmen, virtuelle Computer im Leerlauf identifizieren oder virtuelle Computer im Leerlauf und nicht angefügte Datenträger entfernen. Erstellen Sie mithilfe der Informationen in den Berichten zu Größenempfehlungen und Ineffizienzen einen Plan, um die Größe von virtuellen Computern im Leerlauf zu reduzieren oder diese zu entfernen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem eine Workload getestet und optimiert wurde, ist es an der Zeit, [die Workload für die Höherstufung vorzubereiten](./ready.md).

> [!div class="nextstepaction"]
> [Vorbereiten einer migrierten Workload für die Höherstufung in die Produktion](./ready.md)
